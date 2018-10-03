---
layout: post
title:  "Getting started with Mongoose, a beginner's perspective"
date:   2017-12-22 03:43:00
categories: [coding]
---
<p><a href="https://mongoosejs.com/">Mongoose</a> is an <abbr title="Object Document Mapper">ODM</abbr> that takes away the complexity of all the code you'd have to think and write and that you realise that could be abstracted and reused between all pieces of Entities your application will require.</p>

<h3>Two main features will help you from the beginning</h3>

<ul>
<li>Handles the <b>connection</b> to the MongoDB instance using the official driver behind the scenes</li>
<li>Allows to describe your Entities, or Documents how I should name them better, using <b>Schema</b> implementation that offers you the <b>Model</b>, as expected in the MVC pattern.</li>
</ul>

<p>The <a href="http://mongoosejs.com/docs/guide.html">Schema</a> is what you need to look into first, than <a href="http://mongoosejs.com/docs/models.html">Models</a>.</p>

<p>The Models will allow you to do all CRUD operations, supports pre built in <a href="http://mongoosejs.com/docs/validation.html">Validation</a> that can be extended with any custom rules, comes with built in Getters and Setters and allows any custom ones.</p>

<h3>Clever feature to keep in mind</h3>

<p>Also, Mongoose allows you to hook <b>plugins</b>. This is what DRY really means. Any small problem that can be solved and it's solution reused in Models is a prime candidate to be a plugin. You might be even lucky to find already built <a href="https://www.npmjs.com/search?q=mongoose&amp;page=1&amp;ranking=optimal">Mongoose plugins</a> in the community that are well maintained.</p>

<p>One notable plugin I've found useful is the <a href="https://www.npmjs.com/package/mongoose-version">mongoose-version</a> that helps me implement versioning and moderation states. The quick usage would be like revisions of posts in WordPress.</p>

<h3>Running MongoDB on your local working environment</h3>

<p>My choice for services has been <a href="https://store.docker.com/search?type=edition&amp;offering=community">Docker</a> for many years. Running MongoDB is just one easy thing to run it with Docker. I'm using <a href="https://github.com/docker/kitematic/releases">Kitematic</a> to control my Docker containers and for any project or any test, I'm just starting a new container, a MongoDB container in this case, rename it and on the the container settings, I'm hitting save on the Hostname / Ports page to keep the localhost port persistent between restarts.</p>

<h3>Conclusion</h3>

<p>Mongoose has more features than what I've mentioned as a starting point for a beginner, but those are even for me something to look more in the future. Just the above are decent enough to get me started in describing my main Entities for my second hand cars selling application.</p>

<p>Have fun using MongoDB with this library and feel free to share any other thoughts in comments.</p>
