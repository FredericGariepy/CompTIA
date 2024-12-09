## Network Baseline
A baseline provides quantifiable metrics that are periodically measured with various network performance monitoring tools, protocol analyzers, and packet sniffers. \
Baseline metrics provide a snapshot of normal network operations to help network administrators identify impending problems, troubleshoot current problems, and know when a problem has been fully resolved.

Important metrics might include:
- application response times
- server memory and processor utilization
- average and peak network throughput
- storage input/output operations per second. 

### Network Documentation
Network documentation should include:
- logical and physical diagrams
- application data flows
- change management logs
- user and administration manuals
- warranty and support information

Network baselines and documentation should be updated any time a significant change to the network occurs and as part of the change management process of an organization.

### Logical Troubleshooting Using the OSI Model
Depending on the situation, you might use the bottom-up, top-down, or divide-and-conquer approach when you use the OSI model to guide your troubleshooting efforts. 
+ L1: Confirm physical connectivity
+ L2: Verify data link architectures, such as compatibility with a particular standard or frame type. properly configure security services to allow the required connections.
+ L3: Commonly used ICMP commands include ping and traceroute. Solve for improperly assigned IP addresses,  host cannot communicate with a DHCP, DNS caching services or connection to the wrong DNS servers.
+ L4: Latency and network congestion can interfere with communications that depend on timely acknowledgments and handshakes. Time-to-live (TTL) values sometimes have to be extended in the network service architecture to allow for slower response times during peak network traffic hours. Similar congestion problems can occur when new services are added to an existing network or when a local device triggers a prioritized service, such as a backup or an antivirus scan.
+ L5: Devices that automatically go into a power standby mode (“sleep”) may have expired session tokens that fail when the device attempts to resume connectivity. At the server, failover communications or handshake negotiations with one server may not translate to other clustered servers. Sessions may have to be restarted.
+ L6: layer conflicts are often related to changes in encryption keys or updates to service architectures that are not supported by various client devices. For example, an older browser may not interoperate with a script or a new encoding standard.
+ L7: Many applications may conflict with other apps. Apps also may have caching or corrupted files that can be remedied only by uninstalling and reinstalling or by updating to a newer version. Some apps also require persistent connections to update services or third parties, and network security settings may prevent those connections from being made.

### Common Troubleshooting Problems
+ searching log files for anomalies and significant events
+ verifying that certificates or proper authentication protocols are installed and available
+ verifying encryption settings
+ clearing application caches
+ updating applications
+ for endpoints: removing and reinstalling an application
+ Search vendor-supported sites, forums, (FAQ) pages before you make changes to installed service
+ simply restarting the device
+ restarting a service or rebooting a device may actually compound the problem. Connectivity problems may be intermittent or difficult to trace, so it’s important that your troubleshooting processes follow an approved or standardized methodology.

### Network Documentation
Network documentation should include logical and physical diagrams, application data flows, change management logs, user and administration manuals, and warranty and support information. \
Network baselines and documentation should be updated any time a significant change to the network occurs and as part of the change management process of an organization. 

1. Discover the problem.
2. Evaluat the system configuration against the baseline.
3. Track the possible solutions.
4. Execute a plan.
5. Check the results.
6. Verify the solution (if unsuccessful, return to step 2; if successful, proceed to step 7).
7. Deploy the positive solution.
