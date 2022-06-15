![](/Users/jason/Desktop/pictures/GFC-TS-MACC.png)

1. When running "service wbxd failover" on TS, TS send bridge control request to MACC to failover current bridge;
2. MACC query current/remote bridge load and respond TS if bridge can failover or not; 
   2.1 If current bridge load higher than high-watermark, reject the failover;
   2.2 If current bridge load + remote bridge load higher than 100%, reject the failover.
3. If MACC reject the failover, TS then regards "service wbxd failover" failed; 
4. If MACC allows the failover, TS then follows current failover steps.

| Failover Component | Exception | Maintenance |
| :----------------- | :-------- | :---------- |
| TS                 |           |             |
| TAS                |           |             |
| CMS                |           |             |



![TelephonyFailoverFailbackProcesses](/Users/jason/Desktop/pictures/TelephonyFailoverFailbackProcesses.png)