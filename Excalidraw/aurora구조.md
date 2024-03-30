---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
Cluster Endpoint
(Aurora cluster) ^gCNV1D8a

primary instance ^VB6wwwc5

Reader Endpoint
(Replica loadbalance) ^7UIUcjnh

instance ^6Z7E6r3z


cluster level end point
- Cluster Endpoint
- Reader Endpoint

Cluster endpoint에 요청해도
Aurora는 분산을 위해 읽기 작업을
복제본에게 판단하고 요청할 수 있다. ^dp8OatiL

reader replica를
failover에 사용한다. ^v2OYW9f7

다른 엔진은 클러스터를 쓸건지
인스턴스만 쓸건지 정할 수 있지만
Aurora는 반드시 클러스터를 생성해야 한다. ^rxW3Neyj

Single-Master구조 기준 ^F4Ipd8sz

Aurora Storage Cluster ^wskJE5B3

storage
Node ^ReYgOxCG

storage
Node ^0MTeUNtY

storage
Node ^jIAhboT1

storage
Node ^nsVVo4wZ

storage
Node ^x8iaBxwU

storage
Node ^0XMyDoga

instance ^tozfySgX

Availability Zone 1 ^u5KXbmRO

Availability Zone 2 ^WcwXsbqd

Availabilty Zone3 ^bA58bYrt

각 AZ마다 2개의 데이터 복제본 저장 => 최소 6개의 복제본 ^LxIrRPIz

Quorum모델 사용 (다수결 투표)
만일 6개중 4개의 노드에만기록되었을 경우
완전한 데이터로 인정하겠다 ^prBJkTJm

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.0.25",
	"elements": [
		{
			"type": "rectangle",
			"version": 927,
			"versionNonce": 647907339,
			"isDeleted": false,
			"id": "vdHPc53CDwDqrJzpmuBIb",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "dashed",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 394.67834199235676,
			"y": -391.6738650864917,
			"strokeColor": "#1971c2",
			"backgroundColor": "#e3fafc",
			"width": 268.01051558747577,
			"height": 659.2723331133466,
			"seed": 2019031941,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"id": "qpBMJ7ZOHPS8yke5DHkqj",
					"type": "arrow"
				}
			],
			"updated": 1711814793033,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 849,
			"versionNonce": 361578187,
			"isDeleted": false,
			"id": "XbueB5BrMQkhnq77RDib9",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "dashed",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 112.75099176900858,
			"y": -389.3374739096396,
			"strokeColor": "#1971c2",
			"backgroundColor": "#e3fafc",
			"width": 268.7521358781205,
			"height": 652.8657494021214,
			"seed": 54637035,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1711814792171,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 860,
			"versionNonce": 1447603173,
			"isDeleted": false,
			"id": "Q_w_AoBZ_yVZSb7DKVxcP",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "dashed",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -173.80946623704045,
			"y": -554.7283972702157,
			"strokeColor": "#1971c2",
			"backgroundColor": "#e3fafc",
			"width": 270.5064810998914,
			"height": 821.6678868715065,
			"seed": 456202763,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1711814409816,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 387,
			"versionNonce": 1146822475,
			"isDeleted": false,
			"id": "mxfGA4PFie74496ujUVaE",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -145.74068055141413,
			"y": -750.8374029765188,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 222.8491586538462,
			"height": 130.62960196025534,
			"seed": 1609879659,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "gCNV1D8a"
				},
				{
					"id": "B99ErKRdNnm4Ica1EP4Of",
					"type": "arrow"
				}
			],
			"updated": 1711814289905,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 483,
			"versionNonce": 435092971,
			"isDeleted": false,
			"id": "gCNV1D8a",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -114.9960252357215,
			"y": -710.5226019963911,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 161.35984802246094,
			"height": 50,
			"seed": 515260811,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711814289905,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Cluster Endpoint\n(Aurora cluster)",
			"rawText": "Cluster Endpoint\n(Aurora cluster)",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "mxfGA4PFie74496ujUVaE",
			"originalText": "Cluster Endpoint\n(Aurora cluster)",
			"lineHeight": 1.25,
			"baseline": 43
		},
		{
			"type": "rectangle",
			"version": 900,
			"versionNonce": 1718381387,
			"isDeleted": false,
			"id": "SsWZ5l-grMGsiCfkfstF9",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -128.5747045531402,
			"y": -509.572426394191,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 186.4579759755034,
			"height": 143.98300270048517,
			"seed": 389424709,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "VB6wwwc5"
				},
				{
					"id": "B99ErKRdNnm4Ica1EP4Of",
					"type": "arrow"
				},
				{
					"id": "9-oNWiBvL9BKmT4FZTdY6",
					"type": "arrow"
				},
				{
					"id": "-llzfj1-Icniv4a8RQO9V",
					"type": "arrow"
				},
				{
					"id": "cGEUe-1EpHReuGdbdwlN-",
					"type": "arrow"
				},
				{
					"id": "ogZJgV8jQCv2f9WICpjW8",
					"type": "arrow"
				},
				{
					"id": "5C20_l75YxIV5xmhzOWyE",
					"type": "arrow"
				},
				{
					"id": "Ge3BF9PcWbb0PO0bQaAwE",
					"type": "arrow"
				}
			],
			"updated": 1711812604327,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1056,
			"versionNonce": 1432027877,
			"isDeleted": false,
			"id": "VB6wwwc5",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -113.52564820601351,
			"y": -450.0809250439484,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 156.35986328125,
			"height": 25,
			"seed": 1216550309,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711812604327,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "primary instance",
			"rawText": "primary instance",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "SsWZ5l-grMGsiCfkfstF9",
			"originalText": "primary instance",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "arrow",
			"version": 1714,
			"versionNonce": 1286782763,
			"isDeleted": false,
			"id": "B99ErKRdNnm4Ica1EP4Of",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -42.29350797089472,
			"y": -618.8719293130794,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 3.030820779933606,
			"height": 104.97211753122133,
			"seed": 1107806661,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711814289905,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "mxfGA4PFie74496ujUVaE",
				"gap": 1.3358717031840115,
				"focus": 0.08739712642980375
			},
			"endBinding": {
				"elementId": "SsWZ5l-grMGsiCfkfstF9",
				"gap": 4.32738538766705,
				"focus": -0.017978045765526373
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					3.030820779933606,
					104.97211753122133
				]
			]
		},
		{
			"type": "rectangle",
			"version": 1152,
			"versionNonce": 502459557,
			"isDeleted": false,
			"id": "G3uDm0C0xvFNrMXsKBLXB",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 249.06902080962743,
			"y": -564.3173066274019,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 313.1796875,
			"height": 93.18732978290143,
			"seed": 2121137349,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "7UIUcjnh"
				},
				{
					"id": "hLn9G0DQrePqe7qkV39_n",
					"type": "arrow"
				},
				{
					"id": "1rDeONUIBBDo_gJllYXXC",
					"type": "arrow"
				},
				{
					"id": "tPUHSKiHqKM3cBrDXYZyN",
					"type": "arrow"
				},
				{
					"id": "HGD28QM4XB_VkQp-OjaN3",
					"type": "arrow"
				}
			],
			"updated": 1711814309432,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1376,
			"versionNonce": 1016598533,
			"isDeleted": false,
			"id": "7UIUcjnh",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 302.6989417691001,
			"y": -542.7236417359511,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 205.9198455810547,
			"height": 50,
			"seed": 1467751461,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711814309433,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Reader Endpoint\n(Replica loadbalance)",
			"rawText": "Reader Endpoint\n(Replica loadbalance)",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "G3uDm0C0xvFNrMXsKBLXB",
			"originalText": "Reader Endpoint\n(Replica loadbalance)",
			"lineHeight": 1.25,
			"baseline": 43
		},
		{
			"type": "rectangle",
			"version": 1418,
			"versionNonce": 1480035115,
			"isDeleted": false,
			"id": "gQzE4WPuVcpmWlr_Ootbk",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 224.3797954184131,
			"y": -346.66272017177585,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 144.11030614880133,
			"height": 140.02592818860091,
			"seed": 508664421,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "6Z7E6r3z"
				},
				{
					"id": "1rDeONUIBBDo_gJllYXXC",
					"type": "arrow"
				},
				{
					"id": "mmew3nMlbdNVXc6AOUy11",
					"type": "arrow"
				},
				{
					"id": "tPUHSKiHqKM3cBrDXYZyN",
					"type": "arrow"
				}
			],
			"updated": 1711812604327,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1673,
			"versionNonce": 289034501,
			"isDeleted": false,
			"id": "6Z7E6r3z",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 256.6649823673255,
			"y": -289.1497560774754,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 79.53993225097656,
			"height": 25,
			"seed": 201421861,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711812604327,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "instance",
			"rawText": "instance",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "gQzE4WPuVcpmWlr_Ootbk",
			"originalText": "instance",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "arrow",
			"version": 970,
			"versionNonce": 740577163,
			"isDeleted": false,
			"id": "1rDeONUIBBDo_gJllYXXC",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 367.2690285462703,
			"y": -458.29056021111427,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 50.84814110457825,
			"height": 102.70873227503722,
			"seed": 288721675,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711814309988,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "G3uDm0C0xvFNrMXsKBLXB",
				"gap": 12.839416633386122,
				"focus": 0.049921799964113625
			},
			"endBinding": {
				"elementId": "gQzE4WPuVcpmWlr_Ootbk",
				"gap": 8.919107764301202,
				"focus": -0.17889502029982562
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-50.84814110457825,
					102.70873227503722
				]
			]
		},
		{
			"type": "arrow",
			"version": 1226,
			"versionNonce": 2043094603,
			"isDeleted": false,
			"id": "hLn9G0DQrePqe7qkV39_n",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 448.2877835627077,
			"y": -460.4278932101486,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 61.28474052865403,
			"height": 102.01686282552367,
			"seed": 917577899,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711814309988,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "G3uDm0C0xvFNrMXsKBLXB",
				"gap": 10.702083634351766,
				"focus": -0.04448983621892433
			},
			"endBinding": {
				"elementId": "ssZURFtFjWf9daq8xjiQ0",
				"gap": 10.60111354708954,
				"focus": 0.30354716903003476
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					61.28474052865403,
					102.01686282552367
				]
			]
		},
		{
			"type": "text",
			"version": 793,
			"versionNonce": 138677259,
			"isDeleted": false,
			"id": "dp8OatiL",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 87.45858244186638,
			"y": -766.561810887186,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 243.9839324951172,
			"height": 160,
			"seed": 1050164587,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "WFBUnMsKZUHofUmihN701",
					"type": "arrow"
				}
			],
			"updated": 1711814370181,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "\ncluster level end point\n- Cluster Endpoint\n- Reader Endpoint\n\nCluster endpoint에 요청해도\nAurora는 분산을 위해 읽기 작업을\n복제본에게 판단하고 요청할 수 있다.",
			"rawText": "\ncluster level end point\n- Cluster Endpoint\n- Reader Endpoint\n\nCluster endpoint에 요청해도\nAurora는 분산을 위해 읽기 작업을\n복제본에게 판단하고 요청할 수 있다.",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "\ncluster level end point\n- Cluster Endpoint\n- Reader Endpoint\n\nCluster endpoint에 요청해도\nAurora는 분산을 위해 읽기 작업을\n복제본에게 판단하고 요청할 수 있다.",
			"lineHeight": 1.25,
			"baseline": 154
		},
		{
			"type": "text",
			"version": 377,
			"versionNonce": 299720363,
			"isDeleted": false,
			"id": "v2OYW9f7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 573.7236736755927,
			"y": -533.2671503574499,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 140.60792541503906,
			"height": 40,
			"seed": 917692517,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711815030941,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "reader replica를\nfailover에 사용한다.",
			"rawText": "reader replica를\nfailover에 사용한다.",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "reader replica를\nfailover에 사용한다.",
			"lineHeight": 1.25,
			"baseline": 34
		},
		{
			"type": "text",
			"version": 335,
			"versionNonce": 57215243,
			"isDeleted": false,
			"id": "rxW3Neyj",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -166.268034444206,
			"y": -828.3602254951203,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 296.8638916015625,
			"height": 60,
			"seed": 120242155,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711814298836,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "다른 엔진은 클러스터를 쓸건지\n인스턴스만 쓸건지 정할 수 있지만\nAurora는 반드시 클러스터를 생성해야 한다.",
			"rawText": "다른 엔진은 클러스터를 쓸건지\n인스턴스만 쓸건지 정할 수 있지만\nAurora는 반드시 클러스터를 생성해야 한다.",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "다른 엔진은 클러스터를 쓸건지\n인스턴스만 쓸건지 정할 수 있지만\nAurora는 반드시 클러스터를 생성해야 한다.",
			"lineHeight": 1.25,
			"baseline": 54
		},
		{
			"type": "text",
			"version": 488,
			"versionNonce": 1848270245,
			"isDeleted": false,
			"id": "F4Ipd8sz",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -193.58023932007262,
			"y": -870.5468032329435,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 209.87982177734375,
			"height": 25,
			"seed": 1633015845,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711814300518,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Single-Master구조 기준",
			"rawText": "Single-Master구조 기준",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Single-Master구조 기준",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "rectangle",
			"version": 282,
			"versionNonce": 1407131051,
			"isDeleted": false,
			"id": "17i3WJ-wBeuhq_BxlFhJJ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -203.45518313057158,
			"y": -55.78773317132561,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 900.7936409299638,
			"height": 342.6872066070763,
			"seed": 2043444773,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"id": "-llzfj1-Icniv4a8RQO9V",
					"type": "arrow"
				}
			],
			"updated": 1711812604328,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 323,
			"versionNonce": 862660229,
			"isDeleted": false,
			"id": "wskJE5B3",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -189.14038336107774,
			"y": -40.812603220642586,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 328.6358642578125,
			"height": 35,
			"seed": 649679077,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711812604328,
			"link": null,
			"locked": false,
			"fontSize": 28,
			"fontFamily": 1,
			"text": "Aurora Storage Cluster",
			"rawText": "Aurora Storage Cluster",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Aurora Storage Cluster",
			"lineHeight": 1.25,
			"baseline": 25
		},
		{
			"type": "rectangle",
			"version": 308,
			"versionNonce": 1763979339,
			"isDeleted": false,
			"id": "h43ifr2WAf0D7D4aKjpbP",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -168.8425922480073,
			"y": 20.27610783548505,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 123.57695654705674,
			"height": 208.9236861093881,
			"seed": 923375627,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "ReYgOxCG"
				},
				{
					"id": "9-oNWiBvL9BKmT4FZTdY6",
					"type": "arrow"
				}
			],
			"updated": 1711812604328,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 253,
			"versionNonce": 1320029669,
			"isDeleted": false,
			"id": "ReYgOxCG",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -145.1240755223305,
			"y": 99.73795089017909,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 76.13992309570312,
			"height": 50,
			"seed": 1715202725,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711812604328,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "storage\nNode",
			"rawText": "storage\nNode",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "h43ifr2WAf0D7D4aKjpbP",
			"originalText": "storage\nNode",
			"lineHeight": 1.25,
			"baseline": 43
		},
		{
			"type": "rectangle",
			"version": 328,
			"versionNonce": 1164832491,
			"isDeleted": false,
			"id": "bM_RjprX7kMLrgCkMbfkO",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -35.12717658866637,
			"y": 19.079317766299653,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 123.57695654705674,
			"height": 208.9236861093881,
			"seed": 1678957643,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "0MTeUNtY"
				},
				{
					"id": "-llzfj1-Icniv4a8RQO9V",
					"type": "arrow"
				},
				{
					"id": "cGEUe-1EpHReuGdbdwlN-",
					"type": "arrow"
				}
			],
			"updated": 1711812604328,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 272,
			"versionNonce": 64817477,
			"isDeleted": false,
			"id": "0MTeUNtY",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -11.408659862989566,
			"y": 98.5411608209937,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 76.13992309570312,
			"height": 50,
			"seed": 1168579307,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711812604328,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "storage\nNode",
			"rawText": "storage\nNode",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "bM_RjprX7kMLrgCkMbfkO",
			"originalText": "storage\nNode",
			"lineHeight": 1.25,
			"baseline": 43
		},
		{
			"type": "rectangle",
			"version": 400,
			"versionNonce": 2068240779,
			"isDeleted": false,
			"id": "exU5Br7dGIzvBVoUWQIZ8",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 119.95917793705013,
			"y": 21.992575931058752,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 123.57695654705674,
			"height": 208.9236861093881,
			"seed": 963395435,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "jIAhboT1"
				},
				{
					"id": "cGEUe-1EpHReuGdbdwlN-",
					"type": "arrow"
				},
				{
					"id": "ogZJgV8jQCv2f9WICpjW8",
					"type": "arrow"
				},
				{
					"id": "mmew3nMlbdNVXc6AOUy11",
					"type": "arrow"
				}
			],
			"updated": 1711812604328,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 342,
			"versionNonce": 1683331237,
			"isDeleted": false,
			"id": "jIAhboT1",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 143.67769466272694,
			"y": 101.4544189857528,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 76.13992309570312,
			"height": 50,
			"seed": 1814501899,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711812604328,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "storage\nNode",
			"rawText": "storage\nNode",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "exU5Br7dGIzvBVoUWQIZ8",
			"originalText": "storage\nNode",
			"lineHeight": 1.25,
			"baseline": 43
		},
		{
			"type": "rectangle",
			"version": 415,
			"versionNonce": 1743351851,
			"isDeleted": false,
			"id": "e9Aai5mKjUMmg7UVEMjiU",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 253.67459359639105,
			"y": 20.7957858618733,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 123.57695654705674,
			"height": 208.9236861093881,
			"seed": 1139646635,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "nsVVo4wZ"
				},
				{
					"id": "ogZJgV8jQCv2f9WICpjW8",
					"type": "arrow"
				}
			],
			"updated": 1711812604328,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 361,
			"versionNonce": 2042969093,
			"isDeleted": false,
			"id": "nsVVo4wZ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 277.39311032206786,
			"y": 100.25762891656734,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 76.13992309570312,
			"height": 50,
			"seed": 2053788491,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711812604328,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "storage\nNode",
			"rawText": "storage\nNode",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "e9Aai5mKjUMmg7UVEMjiU",
			"originalText": "storage\nNode",
			"lineHeight": 1.25,
			"baseline": 43
		},
		{
			"type": "rectangle",
			"version": 342,
			"versionNonce": 1564488395,
			"isDeleted": false,
			"id": "Esb5Jtx_1HIjs6UCyRx-m",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 400.00805412646275,
			"y": 18.98966784028846,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 123.57695654705674,
			"height": 208.9236861093881,
			"seed": 560551915,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "x8iaBxwU"
				},
				{
					"id": "5C20_l75YxIV5xmhzOWyE",
					"type": "arrow"
				}
			],
			"updated": 1711812604328,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 288,
			"versionNonce": 1009349477,
			"isDeleted": false,
			"id": "x8iaBxwU",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 423.72657085213956,
			"y": 98.4515108949825,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 76.13992309570312,
			"height": 50,
			"seed": 1978475147,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711812604328,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "storage\nNode",
			"rawText": "storage\nNode",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "Esb5Jtx_1HIjs6UCyRx-m",
			"originalText": "storage\nNode",
			"lineHeight": 1.25,
			"baseline": 43
		},
		{
			"type": "rectangle",
			"version": 363,
			"versionNonce": 65207755,
			"isDeleted": false,
			"id": "Z0gO1eGTFBkvR5SCO8D4l",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 533.7234697858037,
			"y": 17.79287777110312,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 123.57695654705674,
			"height": 208.9236861093881,
			"seed": 685676843,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "0XMyDoga"
				},
				{
					"id": "Ge3BF9PcWbb0PO0bQaAwE",
					"type": "arrow"
				},
				{
					"id": "qpBMJ7ZOHPS8yke5DHkqj",
					"type": "arrow"
				}
			],
			"updated": 1711813980121,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 309,
			"versionNonce": 36962027,
			"isDeleted": false,
			"id": "0XMyDoga",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 557.4419865114805,
			"y": 97.25472082579716,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 76.13992309570312,
			"height": 50,
			"seed": 2007514059,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711813980121,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "storage\nNode",
			"rawText": "storage\nNode",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "Z0gO1eGTFBkvR5SCO8D4l",
			"originalText": "storage\nNode",
			"lineHeight": 1.25,
			"baseline": 43
		},
		{
			"type": "arrow",
			"version": 740,
			"versionNonce": 993047787,
			"isDeleted": false,
			"id": "9-oNWiBvL9BKmT4FZTdY6",
			"fillStyle": "solid",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -48.28415100103061,
			"y": -350.12903406914927,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 44.352670544969385,
			"height": 360.0705693286242,
			"seed": 710210757,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711813980121,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "SsWZ5l-grMGsiCfkfstF9",
				"gap": 15.46038962455657,
				"focus": 0.021218211885729928
			},
			"endBinding": {
				"elementId": "h43ifr2WAf0D7D4aKjpbP",
				"gap": 10.334572576010146,
				"focus": 0.003709449142196143
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-44.352670544969385,
					360.0705693286242
				]
			]
		},
		{
			"type": "arrow",
			"version": 969,
			"versionNonce": 1949480491,
			"isDeleted": false,
			"id": "-llzfj1-Icniv4a8RQO9V",
			"fillStyle": "solid",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -46.18905785078889,
			"y": -348.7009022157158,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 56.045310960030406,
			"height": 354.7432618635561,
			"seed": 1790498955,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711813980121,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "SsWZ5l-grMGsiCfkfstF9",
				"gap": 16.888521477990025,
				"focus": 0.23790328348226672
			},
			"endBinding": {
				"elementId": "bM_RjprX7kMLrgCkMbfkO",
				"gap": 13.036958118459381,
				"focus": 0.022459390943088537
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					56.045310960030406,
					354.7432618635561
				]
			]
		},
		{
			"type": "arrow",
			"version": 1132,
			"versionNonce": 521496427,
			"isDeleted": false,
			"id": "cGEUe-1EpHReuGdbdwlN-",
			"fillStyle": "solid",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -44.056044276453946,
			"y": -353.72070372255837,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 205.01139682528424,
			"height": 351.4885280673725,
			"seed": 571595115,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711813980121,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "SsWZ5l-grMGsiCfkfstF9",
				"gap": 11.86871997114747,
				"focus": 0.4261463184719737
			},
			"endBinding": {
				"elementId": "exU5Br7dGIzvBVoUWQIZ8",
				"gap": 24.224751586244622,
				"focus": 0.44220444403722897
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					205.01139682528424,
					351.4885280673725
				]
			]
		},
		{
			"type": "arrow",
			"version": 1241,
			"versionNonce": 63756779,
			"isDeleted": false,
			"id": "ogZJgV8jQCv2f9WICpjW8",
			"fillStyle": "solid",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -44.15411586320826,
			"y": -353.51246321176325,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 336.9470971486111,
			"height": 348.6016406155402,
			"seed": 1116954085,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711813980121,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "SsWZ5l-grMGsiCfkfstF9",
				"gap": 12.076960481942592,
				"focus": 0.5531861836519959
			},
			"endBinding": {
				"elementId": "e9Aai5mKjUMmg7UVEMjiU",
				"gap": 25.706608458096355,
				"focus": 0.633742009038225
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					336.9470971486111,
					348.6016406155402
				]
			]
		},
		{
			"type": "arrow",
			"version": 1415,
			"versionNonce": 1170840363,
			"isDeleted": false,
			"id": "5C20_l75YxIV5xmhzOWyE",
			"fillStyle": "solid",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -42.35793140189173,
			"y": -355.07121203574195,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 478.74631302035743,
			"height": 351.1258840172787,
			"seed": 1531029067,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711813980121,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "SsWZ5l-grMGsiCfkfstF9",
				"gap": 10.518211657963832,
				"focus": 0.6244480065250135
			},
			"endBinding": {
				"elementId": "Esb5Jtx_1HIjs6UCyRx-m",
				"gap": 22.934995858751734,
				"focus": 0.7261473436860031
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					478.74631302035743,
					351.1258840172787
				]
			]
		},
		{
			"type": "arrow",
			"version": 1482,
			"versionNonce": 1540376331,
			"isDeleted": false,
			"id": "Ge3BF9PcWbb0PO0bQaAwE",
			"fillStyle": "solid",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -27.029750691781146,
			"y": -347.2817952888971,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 579.828555318697,
			"height": 343.02016194440165,
			"seed": 2066305835,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711813980121,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "SsWZ5l-grMGsiCfkfstF9",
				"gap": 18.307628404808668,
				"focus": 0.6715141756911491
			},
			"endBinding": {
				"elementId": "Z0gO1eGTFBkvR5SCO8D4l",
				"gap": 22.054511115598586,
				"focus": 0.7179914922549164
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					579.828555318697,
					343.02016194440165
				]
			]
		},
		{
			"type": "rectangle",
			"version": 1562,
			"versionNonce": 1930465419,
			"isDeleted": false,
			"id": "ssZURFtFjWf9daq8xjiQ0",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 451.30575937493063,
			"y": -347.8099168375354,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 144.11030614880133,
			"height": 140.02592818860091,
			"seed": 1345151275,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"type": "text",
					"id": "tozfySgX"
				},
				{
					"id": "hLn9G0DQrePqe7qkV39_n",
					"type": "arrow"
				},
				{
					"id": "HGD28QM4XB_VkQp-OjaN3",
					"type": "arrow"
				},
				{
					"id": "qpBMJ7ZOHPS8yke5DHkqj",
					"type": "arrow"
				}
			],
			"updated": 1711812607983,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1819,
			"versionNonce": 100425355,
			"isDeleted": false,
			"id": "tozfySgX",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 483.590946323843,
			"y": -290.29695274323495,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 79.53993225097656,
			"height": 25,
			"seed": 1507722187,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711812604328,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "instance",
			"rawText": "instance",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "ssZURFtFjWf9daq8xjiQ0",
			"originalText": "instance",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "text",
			"version": 59,
			"versionNonce": 958956555,
			"isDeleted": false,
			"id": "u5KXbmRO",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "dashed",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -157.1607434862501,
			"y": -537.5066355752341,
			"strokeColor": "#1971c2",
			"backgroundColor": "#e3fafc",
			"width": 141.9839324951172,
			"height": 20,
			"seed": 1511579909,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711815015798,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Availability Zone 1",
			"rawText": "Availability Zone 1",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Availability Zone 1",
			"lineHeight": 1.25,
			"baseline": 14
		},
		{
			"type": "text",
			"version": 15,
			"versionNonce": 596689829,
			"isDeleted": false,
			"id": "WcwXsbqd",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "dashed",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 135.20675560811867,
			"y": -367.63861620099,
			"strokeColor": "#1971c2",
			"backgroundColor": "#e3fafc",
			"width": 149.03993225097656,
			"height": 20,
			"seed": 1549622667,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711815012158,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Availability Zone 2",
			"rawText": "Availability Zone 2",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Availability Zone 2",
			"lineHeight": 1.25,
			"baseline": 14
		},
		{
			"type": "text",
			"version": 51,
			"versionNonce": 1006388709,
			"isDeleted": false,
			"id": "bA58bYrt",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "dashed",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 412.9768967243093,
			"y": -369.1500018248199,
			"strokeColor": "#1971c2",
			"backgroundColor": "#e3fafc",
			"width": 137.03993225097656,
			"height": 20,
			"seed": 617566347,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "HGD28QM4XB_VkQp-OjaN3",
					"type": "arrow"
				}
			],
			"updated": 1711815014690,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Availabilty Zone3",
			"rawText": "Availabilty Zone3",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Availabilty Zone3",
			"lineHeight": 1.25,
			"baseline": 14
		},
		{
			"type": "arrow",
			"version": 70,
			"versionNonce": 1600964779,
			"isDeleted": false,
			"id": "mmew3nMlbdNVXc6AOUy11",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 196.79917510133993,
			"y": -7.0267940091946315,
			"strokeColor": "#e03131",
			"backgroundColor": "#e3fafc",
			"width": 76.64353738950064,
			"height": 190.49467720337134,
			"seed": 1310346699,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711813980121,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "exU5Br7dGIzvBVoUWQIZ8",
				"gap": 29.019369940253398,
				"focus": -0.37231881891958585
			},
			"endBinding": {
				"elementId": "gQzE4WPuVcpmWlr_Ootbk",
				"gap": 9.115320770608946,
				"focus": -0.08824421646088723
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					76.64353738950064,
					-190.49467720337134
				]
			]
		},
		{
			"type": "arrow",
			"version": 116,
			"versionNonce": 1102588107,
			"isDeleted": false,
			"id": "tPUHSKiHqKM3cBrDXYZyN",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 300.69938191956976,
			"y": -357.3071884013651,
			"strokeColor": "#e03131",
			"backgroundColor": "#e3fafc",
			"width": 41.56354342022843,
			"height": 101.80802942976123,
			"seed": 1142380101,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711814309988,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "gQzE4WPuVcpmWlr_Ootbk",
				"gap": 10.644468229589279,
				"focus": -0.2848781697593371
			},
			"endBinding": {
				"elementId": "G3uDm0C0xvFNrMXsKBLXB",
				"gap": 12.014759013374032,
				"focus": 0.22475021095245568
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					41.56354342022843,
					-101.80802942976123
				]
			]
		},
		{
			"type": "arrow",
			"version": 254,
			"versionNonce": 225824933,
			"isDeleted": false,
			"id": "HGD28QM4XB_VkQp-OjaN3",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 521.7430135464175,
			"y": -370.1500018248199,
			"strokeColor": "#e03131",
			"backgroundColor": "#e3fafc",
			"width": 61.18499373648547,
			"height": 88.95329317703704,
			"seed": 1892223723,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711815014690,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "bA58bYrt",
				"gap": 1,
				"focus": 0.6341864682646062
			},
			"endBinding": {
				"elementId": "G3uDm0C0xvFNrMXsKBLXB",
				"gap": 12.026681842643427,
				"focus": -0.0772809246880062
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-61.18499373648547,
					-88.95329317703704
				]
			]
		},
		{
			"type": "arrow",
			"version": 215,
			"versionNonce": 1831055723,
			"isDeleted": false,
			"id": "qpBMJ7ZOHPS8yke5DHkqj",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 589.7003949435291,
			"y": -8.403397209477717,
			"strokeColor": "#e03131",
			"backgroundColor": "#e3fafc",
			"width": 60.09757352367615,
			"height": 190.16161682361349,
			"seed": 181866789,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711813980121,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "Z0gO1eGTFBkvR5SCO8D4l",
				"gap": 26.196274980580853,
				"focus": 0.3742630194026887
			},
			"endBinding": {
				"elementId": "ssZURFtFjWf9daq8xjiQ0",
				"gap": 9.21897461584328,
				"focus": 0.19959402114776592
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-60.09757352367615,
					-190.16161682361349
				]
			]
		},
		{
			"type": "text",
			"version": 220,
			"versionNonce": 924063083,
			"isDeleted": false,
			"id": "LxIrRPIz",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -188.64287938240312,
			"y": 302.9413994187212,
			"strokeColor": "#1971c2",
			"backgroundColor": "#e3fafc",
			"width": 411.3118896484375,
			"height": 20,
			"seed": 982548747,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711812927441,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "각 AZ마다 2개의 데이터 복제본 저장 => 최소 6개의 복제본",
			"rawText": "각 AZ마다 2개의 데이터 복제본 저장 => 최소 6개의 복제본",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "각 AZ마다 2개의 데이터 복제본 저장 => 최소 6개의 복제본",
			"lineHeight": 1.25,
			"baseline": 14
		},
		{
			"type": "text",
			"version": 652,
			"versionNonce": 229119979,
			"isDeleted": false,
			"id": "prBJkTJm",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 415.0250939240681,
			"y": 306.16891309875496,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e3fafc",
			"width": 287.7599182128906,
			"height": 60,
			"seed": 1873086405,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711813041997,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Quorum모델 사용 (다수결 투표)\n만일 6개중 4개의 노드에만기록되었을 경우\n완전한 데이터로 인정하겠다",
			"rawText": "Quorum모델 사용 (다수결 투표)\n만일 6개중 4개의 노드에만기록되었을 경우\n완전한 데이터로 인정하겠다",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Quorum모델 사용 (다수결 투표)\n만일 6개중 4개의 노드에만기록되었을 경우\n완전한 데이터로 인정하겠다",
			"lineHeight": 1.25,
			"baseline": 54
		},
		{
			"id": "WFBUnMsKZUHofUmihN701",
			"type": "arrow",
			"x": 80.76304172645409,
			"y": -615.1255124155135,
			"width": 144.63273444511054,
			"height": 88.61384910882146,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e3fafc",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "dashed",
			"roughness": 2,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1453996203,
			"version": 139,
			"versionNonce": 1189296965,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711814373954,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					144.63273444511054,
					88.61384910882146
				]
			],
			"lastCommittedPoint": null,
			"startBinding": {
				"elementId": "dp8OatiL",
				"focus": 0.9711684105640547,
				"gap": 6.695540715412278
			},
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"type": "arrow",
			"version": 991,
			"versionNonce": 1442178891,
			"isDeleted": true,
			"id": "ENdq7CxM4DF7jV-uSgXoN",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 193.8210970819462,
			"y": -580.6351572676261,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 166.26574262328168,
			"height": 36.164839540078674,
			"seed": 325229317,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711814305443,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "dp8OatiL",
				"gap": 23.296832445725357,
				"focus": 1.0160265822288546
			},
			"endBinding": {
				"elementId": "G3uDm0C0xvFNrMXsKBLXB",
				"gap": 16.17765052322261,
				"focus": 0.6300552027279697
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					166.26574262328168,
					36.164839540078674
				]
			]
		},
		{
			"type": "arrow",
			"version": 273,
			"versionNonce": 1005006955,
			"isDeleted": true,
			"id": "A-t_2JdwePsef68R2ILl1",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 378.1930863495797,
			"y": -547.6361845529292,
			"strokeColor": "#e03131",
			"backgroundColor": "#e3fafc",
			"width": 180.62305054882955,
			"height": 69.13479002238932,
			"seed": 694853643,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711814294249,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "G3uDm0C0xvFNrMXsKBLXB",
				"gap": 19.343517348604337,
				"focus": 0.48653491465514975
			},
			"endBinding": {
				"elementId": "dp8OatiL",
				"gap": 23.296832445725357,
				"focus": 1.140115711753227
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-180.62305054882955,
					-69.13479002238932
				]
			]
		}
	],
	"appState": {
		"theme": "light",
		"viewBackgroundColor": "#ffffff",
		"currentItemStrokeColor": "#1e1e1e",
		"currentItemBackgroundColor": "#e3fafc",
		"currentItemFillStyle": "hachure",
		"currentItemStrokeWidth": 1,
		"currentItemStrokeStyle": "dashed",
		"currentItemRoughness": 2,
		"currentItemOpacity": 100,
		"currentItemFontFamily": 1,
		"currentItemFontSize": 16,
		"currentItemTextAlign": "left",
		"currentItemStartArrowhead": null,
		"currentItemEndArrowhead": "arrow",
		"scrollX": 292.7853983694612,
		"scrollY": 1043.4090742137444,
		"zoom": {
			"value": 1.1511595465580382
		},
		"currentItemRoundness": "round",
		"gridSize": null,
		"gridColor": {
			"Bold": "#C9C9C9FF",
			"Regular": "#EDEDEDFF"
		},
		"currentStrokeOptions": null,
		"previousGridSize": null,
		"frameRendering": {
			"enabled": true,
			"clip": true,
			"name": true,
			"outline": true
		}
	},
	"files": {}
}
```
%%