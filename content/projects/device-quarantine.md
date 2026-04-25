---
title: "Device Quarantine: 0-to-1 ML Security Feature"
date: 2025-06-01
description: "Led an ML-powered security feature from ideation through production -- building novel data labeling and high-precision adversarial detection."
tags: ["ml-engineering", "security", "threat-detection"]
author: "Steven Leung"
---

## Overview

Led the development of a new security feature at Duo Security (Cisco) from ideation through production deployment. The feature detects malicious MFA device registrations with high precision, protecting users from adversarial account takeover.

## The Challenge

The hardest problem wasn't building the model -- it was getting labeled data in a space where none existed. Malicious device registrations were mixed in with legitimate ones, and there was no existing ground truth to train on.

## Approach

- **Data labeling innovation**: Built a labeled data system from scratch by bootstrapping from user fraud reports. This turned sparse, noisy signals into a training dataset precise enough to build high-confidence detectors.
- **High-precision detection**: Developed ML models optimized for precision in an adversarial environment -- where false positives erode trust and false negatives let attackers through.
- **Cross-functional delivery**: Drove the feature across design, engineering, and product teams -- from proving the concept was viable through production deployment.

## Impact

Shipped as a production feature in Duo Security's product, protecting customers from adversarial MFA device registration attacks.

## What I Learned

Working in messy, unlabeled data spaces forces you to be creative about where signal comes from. The data labeling approach I built here -- bootstrapping from indirect signals when direct labels don't exist -- is a pattern I've applied repeatedly since.
