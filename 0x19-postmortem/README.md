Issue Summary

On September 23, 2024, from 14:30 UTC to 17:15 UTC (2 hours and 45 minutes), our e-commerce platform experienced intermittent slowdowns and failures, impacting 60% of users. Affected users were unable to browse products or complete transactions, leading to a 15% decrease in revenue during the outage. The root cause was a memory leak in the Nginx server, triggered by a newly deployed caching mechanism.

Timeline

14:30 UTC – Monitoring system detected increased server response times.
14:32 UTC – On-call engineer confirmed server issues with high response times and 500 errors.
14:35 UTC – Initial investigation focused on the database, suspecting slow queries due to traffic spikes.
14:50 UTC – Database was ruled out as query times were normal, but issues persisted.
15:05 UTC – Frontend team suspected a CDN issue, which was ruled out after testing.
15:30 UTC – Backend investigation focused on Nginx after noticing memory spikes.
16:00 UTC – Identified a memory leak caused by the new caching mechanism.
16:30 UTC – The caching mechanism was disabled, and Nginx was restarted.
17:15 UTC – Full service restored.
Root Cause and Resolution

The issue stemmed from a memory leak in the Nginx server due to improper memory handling in a newly deployed caching system. The caching mechanism retained cached assets for too long, causing memory exhaustion. Disabling the mechanism and restarting Nginx cleared the memory, restoring normal performance. A permanent patch is being developed to fix the caching issue.

Corrective and Preventative Measures

Caching Fix: Refactor the caching mechanism to ensure proper memory handling.
Monitoring Improvement: Add detailed memory usage monitoring for early leak detection.
Rollback Procedures: Develop a rollback procedure to quickly disable problematic features.
Testing Enhancements: Conduct more rigorous stress testing on features that impact server memory.
TODO:

Patch the Nginx caching mechanism.
Add memory monitoring on the Nginx server.
Implement rollback procedures in the deployment pipeline.
Conduct stress tests for memory-intensive deployments.
