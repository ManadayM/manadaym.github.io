---
layout: ../layouts/ResumeLayout.astro
title: "Resume"
---

<div class="pdf-container">
  <object data="./ResumeManadayMavani.pdf" type="application/pdf">
    <p>
      It appears you don't have a PDF plugin to view this document. No worries.. you can <a href="./ResumeManadayMavani.pdf">click here to download the resume in PDF format.</a>
    </p>
  </object>
</div>

<style>
  /* this does some magic that preserves the 8.5x11" aspect ratio */
  .pdf-container {
    height: 0;
    width: 100%;
    padding-bottom: 129.41%; /* 11/8.5 = 1.2941 */
    overflow: hidden;
    position: relative;
  }

  .pdf-container object {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
  }
</style>
