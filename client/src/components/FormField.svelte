<script>
export let value;
export let name
export let placeholder
export let labelName


</script>


<div>
    <div class="flex items-center gap-2 mb-2">
      <label
        for={name}
        class="block text-sm font-medium text-gray-900"
      > {labelName} </label>
    </div>
    <input
      type="text"
      id={name}
      name={name}
      placeholder={placeholder}
      bind:value={value}
      
      
      required
      class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-[#4649ff] focus:border-[#4649ff] outline-none block w-full p-3"
    />
  </div>