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

Writer인스턴스가 데이터를 작성하면,
Aurora 스토리지 엔진은 자동으로 여러 물리적 위치에 데이터를 동기화 하고
이 데이터는 모든 스토리지 노드를 통해 동시에 접근이 가능하다. ^EUkN3AfD

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.0.4",
	"elements": [
		{
			"type": "rectangle",
			"version": 928,
			"versionNonce": 1893196068,
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
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 850,
			"versionNonce": 300757788,
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
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 861,
			"versionNonce": 889724068,
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
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 389,
			"versionNonce": 345010076,
			"isDeleted": false,
			"id": "mxfGA4PFie74496ujUVaE",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -145.74068055141413,
			"y": -750.8374029765189,
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
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 485,
			"versionNonce": 245688356,
			"isDeleted": false,
			"id": "gCNV1D8a",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -114.9960252357215,
			"y": -710.5226019963912,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 161.35984802246094,
			"height": 50,
			"seed": 515260811,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1713696214414,
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
			"baseline": 42
		},
		{
			"type": "rectangle",
			"version": 906,
			"versionNonce": 1217928220,
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
				}
			],
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1057,
			"versionNonce": 1100759972,
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
			"updated": 1713696214414,
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
			"baseline": 17
		},
		{
			"type": "arrow",
			"version": 1723,
			"versionNonce": 1744189596,
			"isDeleted": false,
			"id": "B99ErKRdNnm4Ica1EP4Of",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -42.294397196252305,
			"y": -618.8719293130796,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 3.0313320143193394,
			"height": 104.97211753122144,
			"seed": 1107806661,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1713696214414,
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
					3.0313320143193394,
					104.97211753122144
				]
			]
		},
		{
			"type": "rectangle",
			"version": 1153,
			"versionNonce": 1679568676,
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
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1377,
			"versionNonce": 509396252,
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
			"updated": 1713696214414,
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
			"baseline": 42
		},
		{
			"type": "rectangle",
			"version": 1419,
			"versionNonce": 378710692,
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
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1674,
			"versionNonce": 1363001756,
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
			"updated": 1713696214414,
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
			"baseline": 17
		},
		{
			"type": "arrow",
			"version": 979,
			"versionNonce": 1001240100,
			"isDeleted": false,
			"id": "1rDeONUIBBDo_gJllYXXC",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 367.26718227596774,
			"y": -458.29056021111427,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 50.8470198134591,
			"height": 102.70873227503722,
			"seed": 288721675,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1713696214414,
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
					-50.8470198134591,
					102.70873227503722
				]
			]
		},
		{
			"type": "arrow",
			"version": 1235,
			"versionNonce": 1741368860,
			"isDeleted": false,
			"id": "hLn9G0DQrePqe7qkV39_n",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 448.2894916664417,
			"y": -460.4278932101486,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 61.2836607369552,
			"height": 102.01686282552367,
			"seed": 917577899,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1713696214414,
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
					61.2836607369552,
					102.01686282552367
				]
			]
		},
		{
			"type": "text",
			"version": 794,
			"versionNonce": 811291044,
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
			"updated": 1713696214414,
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
			"version": 378,
			"versionNonce": 318179996,
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
			"updated": 1713696214414,
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
			"version": 336,
			"versionNonce": 63536420,
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
			"updated": 1713696214414,
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
			"version": 489,
			"versionNonce": 359880476,
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
			"updated": 1713696214414,
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
			"baseline": 17
		},
		{
			"type": "rectangle",
			"version": 283,
			"versionNonce": 795228324,
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
			"boundElements": [],
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 324,
			"versionNonce": 196219804,
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
			"updated": 1713696214414,
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
			"baseline": 24
		},
		{
			"type": "rectangle",
			"version": 309,
			"versionNonce": 1323271204,
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
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 254,
			"versionNonce": 870662172,
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
			"updated": 1713696214414,
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
			"baseline": 42
		},
		{
			"type": "rectangle",
			"version": 330,
			"versionNonce": 1478713252,
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
				}
			],
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 273,
			"versionNonce": 905895068,
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
			"updated": 1713696214414,
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
			"baseline": 42
		},
		{
			"type": "rectangle",
			"version": 402,
			"versionNonce": 1398786852,
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
					"id": "mmew3nMlbdNVXc6AOUy11",
					"type": "arrow"
				}
			],
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 343,
			"versionNonce": 1806756124,
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
			"updated": 1713696214414,
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
			"baseline": 42
		},
		{
			"type": "rectangle",
			"version": 417,
			"versionNonce": 318949028,
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
				}
			],
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 362,
			"versionNonce": 678258076,
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
			"updated": 1713696214414,
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
			"baseline": 42
		},
		{
			"type": "rectangle",
			"version": 344,
			"versionNonce": 1807372836,
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
				}
			],
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 289,
			"versionNonce": 23482908,
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
			"updated": 1713696214414,
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
			"baseline": 42
		},
		{
			"type": "rectangle",
			"version": 365,
			"versionNonce": 1819569572,
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
					"id": "qpBMJ7ZOHPS8yke5DHkqj",
					"type": "arrow"
				}
			],
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 310,
			"versionNonce": 361606812,
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
			"updated": 1713696214414,
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
			"baseline": 42
		},
		{
			"type": "arrow",
			"version": 749,
			"versionNonce": 375331108,
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
			"updated": 1713696214414,
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
			"type": "rectangle",
			"version": 1563,
			"versionNonce": 1435859740,
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
			"updated": 1713696214414,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1820,
			"versionNonce": 350770340,
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
			"updated": 1713696214414,
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
			"baseline": 17
		},
		{
			"type": "text",
			"version": 60,
			"versionNonce": 1274001308,
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
			"updated": 1713696214414,
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
			"version": 16,
			"versionNonce": 1975394340,
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
			"updated": 1713696214414,
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
			"version": 52,
			"versionNonce": 1691247644,
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
			"updated": 1713696214414,
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
			"version": 79,
			"versionNonce": 1624144804,
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
			"updated": 1713696214414,
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
			"version": 125,
			"versionNonce": 908296348,
			"isDeleted": false,
			"id": "tPUHSKiHqKM3cBrDXYZyN",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 300.69552964547,
			"y": -357.3071884013651,
			"strokeColor": "#e03131",
			"backgroundColor": "#e3fafc",
			"width": 41.56583844118575,
			"height": 101.80802942976123,
			"seed": 1142380101,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1713696214414,
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
					41.56583844118575,
					-101.80802942976123
				]
			]
		},
		{
			"type": "arrow",
			"version": 259,
			"versionNonce": 1346856740,
			"isDeleted": false,
			"id": "HGD28QM4XB_VkQp-OjaN3",
			"fillStyle": "hachure",
			"strokeWidth": 0.5,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 521.7470675677288,
			"y": -370.1500018248199,
			"strokeColor": "#e03131",
			"backgroundColor": "#e3fafc",
			"width": 61.187379183012354,
			"height": 88.95329317703704,
			"seed": 1892223723,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1713696214414,
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
					-61.187379183012354,
					-88.95329317703704
				]
			]
		},
		{
			"type": "arrow",
			"version": 224,
			"versionNonce": 1201736988,
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
			"updated": 1713696214414,
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
			"version": 221,
			"versionNonce": 1217847972,
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
			"updated": 1713696214414,
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
			"version": 653,
			"versionNonce": 1522076060,
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
			"updated": 1713696214414,
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
			"type": "arrow",
			"version": 140,
			"versionNonce": 275443236,
			"isDeleted": false,
			"id": "WFBUnMsKZUHofUmihN701",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "dashed",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 80.76304172645409,
			"y": -615.1255124155135,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e3fafc",
			"width": 144.63273444511054,
			"height": 88.61384910882146,
			"seed": 1453996203,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1713696214414,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "dp8OatiL",
				"focus": 0.9711684105640547,
				"gap": 6.695540715412278
			},
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					144.63273444511054,
					88.61384910882146
				]
			]
		},
		{
			"type": "text",
			"version": 336,
			"versionNonce": 849180188,
			"isDeleted": false,
			"id": "EUkN3AfD",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "dashed",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": 709.5000671933909,
			"y": -37.92610119824735,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e3fafc",
			"width": 512.39990234375,
			"height": 60,
			"seed": 570498212,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1713696214414,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Writer인스턴스가 데이터를 작성하면,\nAurora 스토리지 엔진은 자동으로 여러 물리적 위치에 데이터를 동기화 하고\n이 데이터는 모든 스토리지 노드를 통해 동시에 접근이 가능하다.",
			"rawText": "Writer인스턴스가 데이터를 작성하면,\nAurora 스토리지 엔진은 자동으로 여러 물리적 위치에 데이터를 동기화 하고\n이 데이터는 모든 스토리지 노드를 통해 동시에 접근이 가능하다.",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Writer인스턴스가 데이터를 작성하면,\nAurora 스토리지 엔진은 자동으로 여러 물리적 위치에 데이터를 동기화 하고\n이 데이터는 모든 스토리지 노드를 통해 동시에 접근이 가능하다.",
			"lineHeight": 1.25,
			"baseline": 54
		},
		{
			"text": "📍[[BackLog]]",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 14,
			"id": "N2JULE6Q",
			"type": "text",
			"x": -4.3666428115602685,
			"y": -515.6192914745633,
			"width": 116.30393981933594,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"roundness": null,
			"seed": 92903,
			"version": 2,
			"versionNonce": 1756465572,
			"updated": 1713696214414,
			"isDeleted": true,
			"groupIds": [],
			"boundElements": [],
			"link": "[[BackLog]]",
			"locked": false,
			"containerId": null,
			"originalText": "📍[[BackLog]]",
			"rawText": "[[BackLog]]",
			"lineHeight": 1.25
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
		"scrollX": 362.96690012520827,
		"scrollY": 945.0166129067878,
		"zoom": {
			"value": 1.0666899465498025
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