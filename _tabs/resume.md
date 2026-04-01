---
layout: page
title: Resume
icon: fas fa-file-pdf
order: 5
---

<div style="display: flex; justify-content: flex-end; margin-bottom: 1rem;">
  <a href="{{ '/assets/resume.pdf' | relative_url }}" class="btn btn-primary" download="Mohammad_Aakil_Iqbal_Resume.pdf" style="text-decoration: none; padding: 8px 16px; border-radius: 4px; background-color: var(--btn-bg); color: var(--btn-text); border: 1px solid var(--btn-border);">
    <i class="fas fa-download"></i> Download PDF
  </a>
</div>

<!-- Embedded PDF Viewer -->
<div class="resume-wrapper" style="width: 100%; height: 850px; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 12px rgba(0,0,0,0.1);">
  <object data="{{ '/assets/resume.pdf' | relative_url }}#view=FitH" type="application/pdf" width="100%" height="100%" style="border: none;">
    <p style="padding: 20px; text-align: center;">Your browser does not support embedded PDFs. <a href="{{ '/assets/resume.pdf' | relative_url }}">Click here to download it.</a></p>
  </object>
</div>