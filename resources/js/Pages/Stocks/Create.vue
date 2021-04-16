<template>
  <div>
    <Layout>
      <div class="flex justify-center full">
        <div class="bg-white flex flex-col w-1/3 mt-20 p-6">
          <h2 class="text-lg">Stock Form</h2>
          <form
            id="stock-form"
            name="stock-form"
            autocomplete="off"
            v-on:submit.prevent="submit"
          >
            <!--* ID -->
            <div class="flex flex-col pt-6">
              <label for="id">ID</label>
              <input class="rounded-md" type="text" id="id" name="id" v-model="form.id" />
              <div class="text-red-700 text-sm">{{ errors.id }}</div>
              {{ form.id }}
            </div>
            <!--* Description -->
            <div class="flex flex-col pt-6">
              <label for="description">Description</label>
              <input
                type="text"
                id="description"
                name="description"
                v-model="form.description"
                class="rounded-md"
              />
              <div class="text-red-700 text-sm">{{ errors.description }}</div>
            </div>
            <!--* Stock Category ID -->
            <div class="flex flex-col pt-6">
              <label for="stock_category_id">Stock Category ID</label>
              <select class="rounded-md" name="stock_category_id" id="stock_category_id" v-model="form.stock_category_id">
                <option value="12259">12259</option>
                <option value="18115">18115</option>
              </select>
              <div class="text-red-700 text-sm">
                {{ errors.stock_category_id }}
              </div>
            </div>
            <!--* UOM -->
            <div class="flex flex-col pt-6">
              <label for="uom">UOM</label>
              <select class="rounded-md" name="uom" id="uom" v-model="form.uom">
                <option value="KIT">KIT</option>
                <option value="RL">RL</option>
                <option value="LOT">LOT</option>
              </select>
              <div class="text-red-700 text-sm">{{ errors.uom }}</div>
            </div>
            <!--* Barcode -->
            <div class="flex flex-col pt-6">
              <label for="barcode">Barcode</label>
              <input
                type="text"
                id="barcode"
                name="barcode"
                v-model="form.barcode"
                class="rounded-md"
              />
              <div class="text-red-700 text-sm">{{ errors.barcode }}</div>
            </div>
            <!--* Discontinued -->
            <div class="flex flex-col pt-6">
              <span for="discontinued">Discontinued</span>
                <div class="mt-2">
                    
                    <input type="radio" id="yes" value="Y" v-model="form.discontinued">
                    <label for="jack"> Yes</label>
                    
                    <input class ="ml-5" type="radio" id="no" value="N" v-model="form.discontinued">
                    <label for="jack"> No</label>
                </div>
              <div class="text-red-700 text-sm">{{ errors.discontinued }}</div>
            </div>

            <!--* Photo Path -->
            <div class="flex flex-col pt-6">
              <label for="photo_path">Photo Path</label>
              <input
                type="text"
                id="photo_path"
                name="photo_path"
                v-model="form.photo_path"
                class="rounded-md"
              />
              <div class="text-red-700 text-sm">{{ errors.photo_path }}</div>
            </div>
            <!--* Button  -->
            <div class="flex flex-col pt-6">
              <button type="submit" class="bg-indigo-800 text-white p-2">
                Save
              </button>
            </div>
          </form>
        </div>
      </div>
    </Layout>
  </div>
</template>

<script>
import { ref, reactive } from "vue";
import Layout from "@/Layouts/Authenticated";
import { Inertia } from "@inertiajs/inertia";
export default {
  components: {
    Layout,
  },
  props: {
    errors: Object,
  },
  setup(props, context) {
    const form = reactive({
      id: null,
      description: null,
      stock_category_id: "12259",
      uom: "KIT",
      barcode: null,
      discontinued: "Y",
      photo_path: "(NULL)",
    });
    const submit = () => {
      Inertia.post(route("stock.store"), form,{
           onSuccess: () => {
                    
                   form.id = null;
                   form.description = null; 
                    form.uom = "KIT";
                    form.barcode = null;
                    form.discontinued = "Y";
                   
                },
      });
    };
    return {
      form,
      submit
    };
  },
};
</script>