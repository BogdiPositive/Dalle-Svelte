<script>
    export let photo;
    export let prompt;
    export let name;

</script>

<div class='rounded-xl group relative shadow-card hover:shadow-cardhover card'>
    <img  class='w-full h-auto object-cover rounded-lg' src={photo} alt={prompt}/>
     <div class='group-hover:flex flex-col max-h-[94.5%] hidden absolute bottom-0 left-0 reght-0 bg-[#10131f] m-2 p-4 rounded-md'>
      <p class='text-white text-md overflow-y-auto prompt'>{prompt}</p>
      <div class='mt-5 flex justify-between items-center gap-2'>
        <div class='flex items-center gap-2'>
          <div class='w-7 h-7 object-cover rounded-full bg-green-700 flex justify-center items-center text-white text-xs font-bold'>
            {name[0]}
          </div>
          <p class='text-white text-sm'>{name}</p>
        </div>
      </div>
     </div>
  </div>