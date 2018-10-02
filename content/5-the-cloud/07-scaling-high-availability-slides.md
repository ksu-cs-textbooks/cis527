---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 5 - Scaling & High Availability</p>
</section>
<section>
	<img class="stretch plain" src="/images/scaling_so.png">
	<p class="imagecredit">Image Source: <a href="https://stackoverflow.com/questions/11707879/difference-between-scaling-horizontally-and-vertically-for-databases">Nati Shalom on Stack Overflow</a></p>
</section>
<section>
	<h3>Scaling</h3>
	<ul>
		<li><b>Horizontal</b> - Add More Droplets & Load Balancer</li>
		<li><b>Vertical</b> - Resize Droplet; Requires Downtime or Existing Infrastructure</li>
	</ul>
</section>
<section>
	<h3>Horizontal Scaling</h3>
	<img class="stretch plain" src="/images/doproxy_do.png">
	<p class="imagecredit">Image Source: <a href="https://www.digitalocean.com/community/tutorials/how-to-automate-the-scaling-of-your-web-application-on-digitalocean-1604">DigitalOcean</a></p>
</section>
<section>
	<h3>AWS Auto Scaling</h3>
	<img class="stretch plain" src="/images/scaling_aws.png">
	<p class="imagecredit">Image Source: <a href="https://aws.amazon.com/autoscaling/">Amazon Web Services</a></p>
</section>
<section>
	<h3>High Availability</h3>
	<img class="stretch plain" src="/images/high_available_do.gif">
	<p class="imagecredit">Image Source: <a href="https://www.digitalocean.com/community/tutorials/what-is-high-availability">DigitalOcean</a></p>
</section>
<section>
	<h3>Case Study</h3>
	<img class="stretch plain" src="/images/netflix_logo.png">
	<p class="imagecredit">Image Source: <a href="https://www.netflix.com">Netflix</a></p>
</section>
<section>
	<img class="stretch plain" src="/images/netflix_hours.png">
	<p class="imagecredit">Image Source: <a href="https://media.netflix.com/en/company-blog/completing-the-netflix-cloud-migration">Netflix</a></p>
</section>
<section>
	<img class="stretch plain" src="/images/netflix_daily.png">
	<p class="imagecredit">Image Source: <a href="https://medium.com/netflix-techblog/scryer-netflixs-predictive-auto-scaling-engine-a3f8fc922270">Netflix Tech Blog</a></p>
</section>
<section>
	<img class="stretch plain" src="/images/netflix_scryer.png">
	<p class="imagecredit">Image Source: <a href="https://medium.com/netflix-techblog/scryer-netflixs-predictive-auto-scaling-engine-a3f8fc922270">Netflix Tech Blog</a></p>
</section>
<section>
	<img class="stretch plain" src="/images/netflix_scaled.png">
	<p class="imagecredit">Image Source: <a href="https://medium.com/netflix-techblog/scryer-netflixs-predictive-auto-scaling-engine-a3f8fc922270">Netflix Tech Blog</a></p>
</section>
<section>
	<img class="stretch plain" src="/images/netflix_cache.jpg">
	<p class="imagecredit">Image Source: <a href="http://highscalability.com/blog/2017/12/11/netflix-what-happens-when-you-press-play.html">High Scalability</a></p>
</section>
<section>
	<img class="stretch plain" src="/images/netflix_simian.png">
	<p class="imagecredit">Image Source: <a href="http://brookscanavesi.com/blog/mobile-app-development/technology-trends/chaos-engineering-breaking-things-purpose/">Brooks Canavesi</a></p>
</section>
<section>
	<img class="stretch plain" src="/images/netflix_chaos.png">
	<p class="imagecredit">Image Source: <a href="https://medium.com/netflix-techblog/chaos-engineering-upgraded-878d341f15fa">Netflix Tech Blog</a></p>
</section>
<section>
	<h3>Cloud Design Considerations</h3>
	<ul>
		<li>Scale Up or Scale Out?</li>
		<li>Build Capacity Predictively or Reactively?</li>
		<li>Design for High Availability?</li>
		<li>Plan for Failures and Outages</li>
		<li>Test Failover Procedures</li>
	</ul>
</section>
