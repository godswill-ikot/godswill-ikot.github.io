---
layout: archive
title: "Research"
permalink: /research/
author_profile: true
header:
  og_image: "research/ecdf.png"
---

My academic MSc Cybersecurity at the University of Roehampton, London, investigates OS hardening and vulnerability auditing techniques in Windows and Linux platforms using automated assessment and system security benchmarking. The study and analysis evaluate the effects of Centre for Internet Security (CIS) Benchmarks implemented through granularity using CIS-CAT Lite and Microsoft Security Compliance Tool for Windows operating systems, and employ the same benchmark using OpenSCAP and CIS-CAT Lite for Linux system analysis. 

This study utilised systematic implementation and testing across controlled virtual environments to examine adherence increase, security posture, performance impact, and operational check. The research methodology encircles foundational security assessments, progressive CIS-benchmark utilisation (Level 1 and 2), conformance validation, and quantitative cross-platform analysis.  

The results present significant security improvements across both platforms, with Ubuntu 20.04 achieving +26% and +25% from (59 - 85)% and (60 - 85)% for Level 1 before and after hardening, more increase were seen in Level 2 CIS Benchmarks, whose results are +27 and +36 from (51 - 78)% and (40 - 76)% for CIS-CAT and OpenSCAP, respectively.  

The findings of this research stress the growing need for standard security evaluation systems independent of personal and enterprise environments characterised by the coexistence of two or more operating systems. By applying the tools on an organised basis and critically analysing the results, the research showed how effective the tools are in highlighting inadequate security configurations, attack vectors, unplugged compliance holes, and potential security holes in both OS’s. 

Key results and findings showed that automated benchmarking tools offer substantial benefits to maintain stable and better security postures, such as strong cross-platform support and compatibility in CIS-CAT Lite. The study develops and recommends the best practice tool integration, reporting, and remediation practices. OpenSCAP turned out to be effective on Linux-based systems as a result of its native SCAP compliance, and Windows-specific checkmate was as a result of a combination of CIS-CAT (Lite) and security features in place.  

The research contributes interesting values in cybersecurity by providing inherent evidence of the effect of the tool, by creating evaluation approaches, and by constructing policies and frameworks for sustained security monitoring. Experience demonstrated that tremendous security improvements can be achieved by applying these benchmarking tools in an incremental phased manner by individuals and organisations, via measurable reductions in security risk exposure and enhanced conformance postures. 
<nbsp>

{% include base_path %}

{% assign ordered_pages = site.research | sort:"order_number" %}

{% for post in ordered_pages %}
  {% include archive-single.html type="grid" %}
{% endfor %}
