---
layout: post
title:  "�۳Ъ��s�޳N���� 3MAD"
date:   2017-06-11 15:00:00 +0800
---

# �۳Ъ��s�޳N���� 3MAD

## �o�ӧ޳N���ХD�n�O�Q�ΤT�����u�ݺ��^�A���L�L���ɽu�]�ײv�^�n�ۤv��

## ���T�ӰѼƥi�H�վ�: ���O�O���T�����u�M�Ĥ@�G�����u�t���[�v 

```
Inputs:
	Near(5),
	Middle(10),
	Far(20),
	NearMAWeight(0.5); // Slope of MA to Entry
Vars: 
	NearMA(0),
	MiddleMA(0),
	FarMA(0),
	NearDiff(0), 
	FarDiff(0),
	Diff(0);

// MA*3
NearMA = Average(Close, Near);
MiddleMA = Average(Close, Middle);
FarMA = Average(Close, Far);
//Slopes of MA
NearDiff = NearMA - MiddleMA;
FarDiff = MiddleMA - FarMA;
// Ouvek MA*3 Diff Band
Diff = (NearDiff * NearMAWeight) + FarDiff;

plot1(Diff, "OuvekMADiff");
```