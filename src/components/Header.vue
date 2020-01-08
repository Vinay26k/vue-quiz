<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled>
        <b>Quiz Application</b>
      </b-nav-item>
      <b-nav-item disabled>Attempted: {{numTotal}}/{{total}}</b-nav-item>
    </b-nav>
  </div>
</template>
<script>
export default {
  props: ["numTotal", "total"]
};
</script>