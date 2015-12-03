---
title: Basic Block Data Decomposition in Perl
author: lbjay
layout: post
permalink: /archives/65
categories:
  - code
  - hacks
  - parallel
tags:
  - perl parallel threads
---
<abbr class="unapi-id" title=""><!-- &nbsp; --></abbr> 

I was playing around with the idea of parallelizing something the other day to eke out some performance. Unfortunately, I&#8217;ve gotten a bit rusty since writing some MPI code for a parallel computing course a few years back. I got stuck on what should be the simple part of dividing up my input across the threads.

<!--more-->The goal is to divvy things up into continguous blocks of roughly equal size. i.e., if the size of your input is 38 (

*n*) and you start four threads (*p*) you don&#8217;t want to give the first three threads chunks of 12 and the last thread gets 2. You want slices of 10, 9, 10 and 9.

So I flailed away with loops and the POSIX::floor for little awhile and came pretty close to what I remembered. I had to finally drag out my [textbook][1] (and translate from the C Macros) to get it right.

<pre lang="perl">#!/usr/bin/perl

# Block Data Decomposition:
# Divide array n into p contiguous blocks of roughly equal size

use POSIX qw(floor);
use strict;

sub block_start {
    my ($i, $p, $n) = @_;
    return floor(($i * $n) / $p);
}

sub block_end {
    my ($i, $p, $n) = @_;
    return (block_start($i + 1, $p, $n) - 1);
}

my @input = get_input();
my $n = scalar @input;
my $p = 4;

for my $i (0..$p-1)
{
    my $start = block_start($i, $p, $n);
    my $end = block_end($i, $p, $n);
    my @range = @input[$start..$end];
    do_something(\@range);
}</pre>

The idea is that

<div class="codecolorer-container text default" style="overflow:auto;white-space:nowrap;width:435px;">
  <div class="text codecolorer">
    do_something(\@range)
  </div>
</div>

sends a slice of input off for processing by one of your threads. A pretty useful algorithm when doing this sort of thing. Certainly not rocket science. Which is why we should all be happy I&#8217;m not a rocket scientist.

 [1]: http://books.google.com/books?id=tDxNyGSXg5IC