---
layout: archive
title: "Research"
permalink: /research/
author_profile: true
header:
  og_image: "research/ecdf.png"
---

This research investigates OS hardening and vulnerability auditing techniques in Windows and Linux platforms featuring automated assessment and system security benchmarking. The research and analysis evaluate the effectiveness of Center for Internet Security (CIS) Benchmarks implemented through granularity using CIS-CAT Lite and Microsoft Security Compliance Tool for Windows operating systems and employ the same benchmark using OpenSCAP and CIS-CAT Lite for Linux system analysis. 

Utilizing systematic implementation and testing across controlled virtual environments, this study examined adherence increase, security posture, performance impact, and operational check. The research methodology encircles foundational security assessments, progressive CIS-benchmark utilization (Level 1 and Level 2), conformance validation, and quantitative cross-platform analysis.  

The results present significant security improvements across both platforms, with Ubuntu 20.04 achieving +26% and +25% from (59 - 85)% and (60 - 85)% for Level 1 before and after hardening, further increase were seen in Level 2 CIS Benchmarks, whose results are +27 and +36 from (51 - 78)% and (40 - 76)% for CIS-CAT and OpenSCAP, respectively.  

The findings of the research stress the growing need for standard security evaluation systems independent of personal and enterprise environments characterized by the coexistence of two or more operating systems. By applying the tools on an organized basis and critically analysing the results, the research showed how effective the tools are in highlighting inadequate security configurations, attack vectors, unplugged compliance holes, and potential security holes in both OS’s. 

 

Key results and findings showed that automated benchmarking tools offer substantial benefits to maintain stable and better security postures, such as strong cross-platform support and compatibility in CIS-CAT Lite. The study develops and recommends the best practice tool integration, reporting, and remediation practices. OpenSCAP turned out to be effective on Linux-based systems as a result of its native SCAP compliance, and Windows-specific checkmate was as a result of a combination of CIS-CAT (Lite) and security features in place. 

 

The research contributes interesting values in cybersecurity by providing inherent evidence of the effectiveness of the tool, by creating evaluation approaches, and, constructing policies and frameworks for sustained security monitoring. Experience demonstrated that tremendous security improvements can be achieved by applying these benchmarking tools in an incremental phased manner by both individuals and organizations, via measurable reductions in security risk exposure and enhanced conformance postures. 
<nbsp>

{% include base_path %}

{% assign ordered_pages = site.research | sort:"order_number" %}

{% for post in ordered_pages %}
  {% include archive-single.html type="grid" %}
{% endfor %}
