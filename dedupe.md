--- 
layout: page 
title: 
description: 
permalink: /projects/dedupe/ 
img: 
---

<link rel="stylesheet" href="{{site.baseurl}}/font-awesome/css/font-awesome.min.css">
<link rel="stylesheet" type="text/css" href="{{ site.baseurl }}/project_description.css" />
<script src="{{site.baseurl}}/bootstrap/js/jquery.min.js"></script>
<script src="{{site.baseurl}}/bootstrap/js/popper.min.js"></script>
<script src="{{site.baseurl}}/bootstrap/js/bootstrap.min.js"></script>


<div class="row">
<div class="col-md-12">
<h4 class="uppercase" style="margin-top:auto; margin-bottom:auto;">Dedupe Portal</h4>
</div>
<div class="col-md-8">
<h5> Web App that provides a rich interface to deduplicate people data using active learning 
techniques in the backend.
</h5>
</div>
<div class="col-md-4"></div>
<hr class="mb32">
</div>

<div class="row">
<div class="col-md-12">
<p>Collaborators:
<a href="https://github.com/anshul-goyal" target="_blank">Anshul Goyal</a>,
<a href="https://github.com/vin29g" target="_blank"> Vinay Gedam</a>.
</p>
</div>
</div>

<div class="row">
<div class="col-md-6">

<div class="row">
<div id="myCarousel" class="carousel slide" data-ride="carousel">
<ol class="carousel-indicators">
<li data-target="#myCarousel" data-slide-to="0" class="active"></li>
<li data-target="#myCarousel" data-slide-to="1"></li>
<li data-target="#myCarousel" data-slide-to="2"></li>
<li data-target="#myCarousel" data-slide-to="3"></li>
<li data-target="#myCarousel" data-slide-to="4"></li>
</ol>
<div class="carousel-inner">
<div class="carousel-item active">
<img src="{{site.baseurl}}/images/dedupe/csv.jpg" alt="Dedupe Snapshots" style="width:460px; height:307px; ">
</div>
<div class="carousel-item">
<img src="{{site.baseurl}}/images/dedupe/IMG_8832.JPG" alt="Dedupe Snapshots" style="width:460px; height:307px;">
</div>
<div class="carousel-item">
<img src="{{site.baseurl}}/images/dedupe/IMG_8833.JPG" alt="Dedupe Snapshots" style="width:460px; height:307px;">
</div>
<div class="carousel-item">
<img src="{{site.baseurl}}/images/dedupe/IMG_8845.JPG" alt="Dedupe Snapshots" style="width:460px; height:307px;">
</div>
<div class="carousel-item">
<img src="{{site.baseurl}}/images/dedupe/IMG_8846.JPG" alt="Dedupe Snapshots" style="width:460px; height:307px;">
</div>
</div>
        
</div>
<a class="carousel-control-prev" href="#myCarousel" data-slide="prev">
<span class="carousel-control-prev-icon"></span>
</a>
<a class="carousel-control-next" href="#myCarousel" data-slide="next">
<span class="carousel-control-next-icon"></span>
</a>
</div>
</div>

<div class="col-md-6">
<h4 class="uppercase mb-xs-24">Background</h4>
<p>
Data deduplication -- often called intelligent compression or single-instance storage -- 
is a process that eliminates redundant copies of data and reduces storage overhead. 
Data deduplication techniques ensure that only one unique instance of data is retained on storage
media, such as DB, disk, flash or tape. Redundant data blocks are replaced with a pointer 
to the unique data copy.
</p>

<h4 class="uppercase mb-xs-24">Objectives</h4>
<p>
In this project, we aim to deduplicate people data to consolidate user profiles collected from
multiple paltforms. We identify and merge all duplicates to create one enriched copy and
delete all other redundant copies. The project uses dedupe library for the same and provides
a web interface over it which takes a csv file as input, performs deduplication using active
learning technique and finally downloads the deduplicated csv file. 
</p>

<h4 class="uppercase mb-xs-24">Products</h4>
<ul data-bullet="ti-check-box">
<li><i class="fa fa-check-square-o" aria-hidden="true"></i>Web App </li>
</ul>

</div>
</div>


