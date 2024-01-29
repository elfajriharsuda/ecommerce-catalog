<template>
  <footer class="footer">
      <div class="copyright">
        Copyrights &copy; {{ currentYear }} <a href="https://www.linkedin.com/in/elfajriharsuda/" target="_blank">{{ organizationName }}.</a> All rights
            reserved.
      </div>
      <div class="legal-links">
        <a href="#">Terms of Service</a>
        <a href="#">Privacy Policy</a>
        </div>
  </footer>
</template>
<script>
export default {
  data() {
    return {
      currentYear: new Date().getFullYear(),
      organizationName: 'elfajriharsuda', // Replace with your organization name
    };
  },
};
</script>
