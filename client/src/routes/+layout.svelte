<script>
    import logo from "../assets/logo.jpg";
</script>

<header class="w-full flex justify-between items-center bg-white sm:px-8 px-4 py-4 border-b border-b-[#e6ebf4]">
    <a href="/">
      <img src={logo} class="w-16 h-16 object-contain" alt="logo"/>
    </a>
    <a
      href="/create"
      class="font-inter font-medium bg-[#6469ff] text-white px-4 py-2 rounded-md"
    >
      Create
</a>
  </header>
  <slot></slot>