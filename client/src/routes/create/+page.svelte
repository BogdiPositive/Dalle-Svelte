<script>
  import { goto } from "$app/navigation";
  import preview from "../../assets/preview.png";
  import FormField from "../../components/FormField.svelte";
  import Loader from "../../components/Loader.svelte";
  let form = {
    name: "",
    prompt: "",
    photo: "",
  };
  let generatingImage = false;

  let loading = false;

  const handleSubmit = async (e) => {
    e.preventDefault();

    if (form.prompt && form.photo) {
      loading = true;
      try {
        console.log(form)
        const response = await fetch("http://localhost:8080/api/v1/post", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          
          body: JSON.stringify({ ...form }),
        });

        await response.json();
        goto("/");
      } catch (err) {
        alert(err);
      } finally {
        loading = false;
      }
    } else {
      alert("Please generate an image with proper details");
    }
  };

  const generateImage = async () => {
    if (form.prompt) {
      try {
        generatingImage = true;
        const response = await fetch("http://localhost:8080/api/v1/dalle", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            prompt: form.prompt,
          }),
        });
        const data = await response.json();
        form = { ...form, photo: `data:image/jpeg;base64,${data.photo}` };
      } catch (error) {
        alert(error);
      } finally {
        generatingImage = false;
      }
    } else {
      alert("Please enter a prompt");
    }
  };
</script>

<section class="max-w-7xl mx-auto">
  <div class="">
    <h1 class="font-extrabold text-[#222328] text-[32px]">Create</h1>
    <p class="mt-2 text-[#666e75] text-[16px] max-w[500px]">
      Create imagination and visually stunning images through DALL-E AI and
      share them with the community
    </p>
  </div>
  <form class="mt-16 max-w3xl" onSubmit={handleSubmit}>
    <div class="flex flex-col gap-5">
      <FormField
        labelName="Your name"
        name="name"
        placeholder="John Doe"
        bind:value={form.name}
      />
      <FormField
        labelName="Prompt"
        name="prompt"
        placeholder="a pencil and watercolor drawing of a bright city in the future with flying cars"
        bind:value={form.prompt}
        isSurpriseMe
      />

      <div
        class="relative bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 w-64 p-3 h-64 flex justify-center items-center"
      >
        {#if form.photo}
          <img
            src={form.photo}
            alt={form.prompt}
            class="w-full h-full object-contain"
          />
        {:else}
          <img
            src={preview}
            alt="priview"
            class="w-9/12 h-9/12 object-contain opacity-40"
          />
        {/if}
        {#if generatingImage}
          <div
            class="absolute inset-0 z-0 flex justify-center items-center bg-[rgba(0,0,0,0.5)] rounded-lg"
          >
            <Loader />
          </div>
        {/if}
      </div>
    </div>
    <div class="mt-5 flex gap-5">
      <button
        type="button"
        on:click={generateImage}
        class="text-white bg-green-700 font-medium rounded-md text-sm w-full sm:w-auto px-5 py-2.5 text-center"
      >
        {#if generatingImage} Generating... 
       {:else} Generate
       {/if}
      </button>
    </div>
    <div class="mt-10 mb-6">
      <p class="mt-2 text-[#666e75] text-[14px]">
        Once you have created the image you want, you can share it with others
        in the community
      </p>
      <button
        on:click={handleSubmit}
        type="submit"
        class="mt-3 text-white bg-[#6469ff] font-medium rounded-md text-sm w-full sm:w-auto px-5 py-2.5 text-center"
      >
        {#if loading } Loading... {:else} Share with the community {/if}
      </button>
    </div>
  </form>
</section>
