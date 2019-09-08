**HTTrack**

A web crawler and offline browser. It can download the entire contents of a web page and then have the saved information accessible through a web browser. This is useful because we can download the page one time, and then look around entirely locally without sending anymore traffic to the target. It is important to note that there are many different configurations possible such as crawl speed, traversal depth, and filters \(include/exclude\). This is important because remember, we are in our semi-passive recon phase, so while we want to browse and interact normally with the website, this makes it much easier to do further analysis of the mirrored content. SiteSucker is a similar tool which we wont cover, but is nonetheless a viable replacement.



We can even examine the source code. Notice the injected headers that let us know we are looking at mirrored content from HTTrack. Although rarer these days, searching within the HTML source may reveal clear-text credentials left there for testing purposes by administrators or developers. It can also reveal software versions, contact information, and other configuration information may also be found.



