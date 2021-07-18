

What Features Are Involved?
- Crawling Frequency to Differennt Websites
- Deduplication of multiple links
- Protocols supported: HTTPS / FTP / STMP
- Storage of Metadata/Website Content
  - What's the end result after crawling?


1. Input Seed URLs
2. URL Frontiers
   1. How To Prioritize the URLs to crawl?
      1. The quality of a page
      2. The change rate of the page
3. Fetching Data
   1. Producer-Consumer Pattern between step 2 and step 3
   2. Implement Politeness: Not to overwhelming the host’s server
4. DNS Resolver
5. Caches
6. Content Seen Module: Check if the content has already retrieved from other URLs
7. Storage
8. Processing Data
   1. Link Extractor
   2. URL Filtering
   3. URL De-Dup
      1. The Bloom Filter


How to handle frequently changing websites?


Reference
- https://medium.com/double-pointer/top-5-videos-for-web-crawler-system-design-interview-75b7ac9c04ce
- https://github.com/donnemartin/system-design-primer/tree/master/solutions/system_design/web_crawler
- https://www.educative.io/courses/grokking-the-system-design-interview/NE5LpPrWrKv