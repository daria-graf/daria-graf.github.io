---
layout: page
title: Talks
permalink: /talks/
---

# List of my presentations:

## Integration von Usability und Software Engineering (DE)

In dieser Präsentation habe ich über den Einsatz von Design Thinking während des Softwareentwicklungsprozesses gespochen.

[Digital Xchange Bergisches RheinLand 2019](/assets/img/presentations/25052019_Graf_Design_Thinking_DigitalXChange.pdf)

### Über die Konferenz
Rund 800 Besucher, 14 thematische Tracks mit mehr als 100 Expertenvorträgen, eine Podiumsdiskussion mit namhaften Vertretern aus Politik, Wissenschaft und Wirtschaft sowie eine große After-Show-Party in der Halle 32 auf dem Steinmüllergelände – Das war die Digital Xchange 2019!

## E2E-Tests Monitoring: Practical Insights from the OBI Sales-Rep-Tool (ENG)

Monitoring a web-based application can be a tricky business, especially if the application consists of several independent, self-contained services. E2E testing can be a good choice to ensure that all parts of the system are working correctly. But how can we build a reliable test monitoring infrastructure that ensures our tests are running and notifies us when the system encounters problems? How can we have easy and quick access to current and previous test results and get an overview of important test statistics? This presentation will give you a practical insight into a E2E-Test monitoring solution that our team built for the OBI Sales-Rep-Tool web-based application.

Our approach involves running tests as a Docker container in Kubernetes, effectively reducing the burden on our CI/CD GitLab Runner. By converting the test results into customized Prometheus metrics we are able to create a real-time Grafana Dashboard that displays test results and their duration. Additionally, our developer teams receive immediate notifications via Slack, along with error reports containing recorded videos, whenever the system encounters issues. This is facilitated by a simple Node.js Webserver that runs in parallel with the tests and communicates with various APIs.

 [OBI next Tech Talks Meetup 12.December 2023](/assets/img/presentations/12122023_Graf_OBInext_TechTalk_Meetup_E2E-Test-Monitoring.pdf)

### About OBI Tech Talks

OBI Tech Tech Talks is a knowledge and best practicies exchange meetup group for IT professionals based in Cologne (Germany).