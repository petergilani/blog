---
layout: post
title: Cisco - Foundation-sec-8b
---

This last week, on Monday 28th April, Cisco released [Fondation-Sec-8B](https://huggingface.co/fdtn-ai/Foundation-Sec-8B):

[![Fondation-sec-Announcement]({{ site.baseurl }}/images/ai-security.jpeg)](https://blogs.cisco.com/security/foundation-sec-cisco-foundation-ai-first-open-source-security-model)

A notable first for Cisco, spearheaded by their new [Foundation AI Team](https://blogs.cisco.com/security/foundation-ai-building-the-intelligent-future-of-cybersecurity), **Fondation-Sec-8B** is 
 a cybersecurity focused/fine-trained model, off the base [Meta-Llama-3.1-8B](https://huggingface.co/meta-llama/Llama-3.1-8B), for specific use cases:

 1. **SOC Acceleration**:
   - Summarising multi-source alerts into human-readable case notes.
   - Generating incident timelines and identifying relevant entities.
   - Drafting analyst-style reports to support incident resolution and handoffs.

2. **Proactive Threat Defense**:
   - Extracting Tactics, Techniques, and Procedures (TTPs) from threat intelligence reports.
   - Prioritising vulnerabilities based on contextual impact and exploitability.
   - Generating attack path hypotheses from asset and configuration data.
   - Drafting penetration test reports with vulnerability details and remediation steps.

3. **Engineering Enablement**:
   - Interpreting and applying security policies during development and deployment.
   - Validating configuration files and infrastructure setups against best practices.
   - Assessing whether submitted evidence meets compliance control requirements.
   - Analyzing security policies for inconsistencies and outdated controls.

For more details, see the full technical report [here](https://arxiv.org/abs/2504.21039).

Of particular note, was the depth to which the team went to improve the quality of their training data, requiring both significant effort as well as expertise, in order to achieve the impressive improvements they demonstrated over the base Llama model, and even larger/frontier models.

I've been testing the model, alongside other recent releases in the LLM space, over the last few days, and will be updating this post with some hands-on example and additional details as time permits.
