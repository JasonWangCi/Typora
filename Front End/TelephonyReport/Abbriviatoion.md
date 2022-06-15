**Monitor TS status logic:** ( **ZoneStatus.class** )
\1. pri side port down, but gsb side up -- **AUTO**
\2. pri side port down, and gsb side down too -- **INVA**
\3. pri side port up and pri side not all suspend -- **PRIM**
\4. pri side port up and pri side all suspend and manu flag exist -- **MANU**
\5. pri side port up and pri side all suspend and manu flag not exist -- **AUTO** -- do operation on server directly
\6. pri side port up, but all cannot get suspend status -- **INVA**



Zone:

```
healthcheckApi
```

```
@Column(name = "pri_svip")
private String priStaticVip;

@Column(name = "gsb_svip")
private String gsbStaticVip;

@Column(name = "pri_fvip")
private String priFloatVip;

@Column(name = "pri_fvip_port")
private String priFloatVipPort;

@Column(name = "gsb_fvip")
private String gsbFloatVip;

@Column(name = "gsb_fvip_port")
private String gsbFloatVipPort;
```

**MACC** is **M**ulti-media **A**dvance **C**luster **C**ontroller

**TAS**  **T**elephony **A**pplication ***S**erver* : provides the basic call-processing services,

**TS**   **T**elePresence **S**erver  **T**clsh **S**ervice       tacacs-server

CMS - **C**ollaboration **M**edia **S**erver： provide enterprise voice and web conferencing solutions.

ASR - **A**ggregation **S**ervices **R**outers

https://wiki.cisco.com/display/CMS/Collaboration+Media+Server+%28CMS%29+Wiki

ServerManager has a timer to adjust the TAS connection load balance between MACCs, when a new MACC joins, this timer will launch for 3 times





GFC: [gfcqa-ocp.qa.webex.com](https://gfcqa-ocp.qa.webex.com/)  → North America 1 → tsj8(tp1) 

​                          → North America 2 → tta8(tp2) 

​                          → North America 2 → tta8(tp2) 



| **steps** | **Status** | **Action**                              | **notes**                            |
| :-------- | :--------- | :-------------------------------------- | :----------------------------------- |
| step1     | Done       | Start meeting 1 on DC1, phone/voip join | meeting 1 open on DC1                |
| step2     | Done       | Do DC1 failover                         | meeting 1 switch to DC2              |
| step3     | Done       | Start meeting 2                         | meeting 2 should be on DC2           |
| step4     | Done       | Upgrade DC1                             | macc1->macc2->TS1->tas1->tas2->TS2   |
| step5     | Done       | Do DC1 failback                         |                                      |
| step6     | Done       | Start meeting 3                         | meeting 3 should be on DC1           |
| step7     | Done       | Do DC2 failover                         | meeting 1 and 2 should switch to DC1 |
| step8     | Done       | Upgrade DC2                             | macc3->macc4->TS3->tas3->tas4->TS4   |
| step9     | Done       | Do DC2 failback                         |                                      |

<img src="/Users/jason/Library/Application Support/typora-user-images/image-20220309151201538.png" alt="image-20220309151201538" style="zoom:50%;" />