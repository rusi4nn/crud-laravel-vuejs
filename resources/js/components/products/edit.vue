<script setup>
import { onMounted, ref } from "vue"
import { useRouter } from 'vue-router'

let form = ref({

    id:'',
    nome:'',
    descricao:'',
    photo:'',
    tensao:'',
    marca:''

})

onMounted(async () => {
    getsingleProduct()
})

const props = defineProps({
    id:{
        type:String,
        default:''
    }
})

const router = useRouter()

const getPhoto = () => {

    let photo = "/upload/image.png"
    if(form.value.photo) {
        if(form.value.photo.indexOf('base64') != -1) {
            photo = form.value.photo
        } else {
            photo = '/upload/'+form.value.photo
        }
    }
    return photo

}

const updatePhoto = (e) => {
    let file = e.target.files[0];
    let reader = new FileReader();
    let limit = 1024 * 1024 * 2;
    if(file['size'] > limit) {
        return false
    }
    reader.onloadend = (file) => {
        form.value.photo = reader.result;
    }
    reader.readAsDataURL(file);

}

const getsingleProduct = async () => {
    let response = await axios.get('/api/get_edit_product/${props.id}')
    form.value = response.data.product
}

const updateProduct = () => {
    const formData = new FormData()
    formData.append('nome',form.value.nome)
    formData.append('descricao',form.value.descricao)
    formData.append('photo',form.value.photo)
    formData.append('tensao',form.value.tensao)
    formData.append('marca',form.value.marca)

    axios.post('/api/update_product/${form.value.id}', formData)
      .then((response)=> {
          form.value.nome='',
          form.value.descricao='',
          form.value.photo='',
          form.value.tensao='',
          form.value.marca=''

          router.push('/')

          toast.fire({
              icon:"success",
              title:"Produto editado com sucesso"
          })
      })
      .catch((error)=> {

      })
}

</script>

<template>
    <div class="container">
        <div class="products__edit ">
       
                <div class="products__create__titlebar dflex justify-content-between align-items-center">
                    <div class="products__create__titlebar--item">
                        
                        <h1 class="my-1">Editar Produto</h1>
                    </div>
                    <div class="products__create__titlebar--item">
                        
                        <button class="btn btn-secondary ml-1" @click="updateProduct()">
                            Save
                        </button>
                    </div>
                </div>

                <div class="products__create__cardWrapper mt-2">
                    <div class="products__create__main">
                        <div class="products__create__main--addInfo card py-2 px-2 bg-white">
                            <p class="mb-1">Nome</p>
                            <input type="text" class="input" v-model="form.nome">

                            <p class="my-1">Descrição (optional)</p>
                            <textarea cols="10" rows="5" class="textarea" v-model="form.descricao"></textarea>
                            
                            <div class="products__create__main--media--images mt-2">
                                <ul class="products__create__main--media--images--list list-unstyled">
                                    
                                    <li class="products__create__main--media--images--item">
                                        <div class="products__create__main--media--images--item--imgWrapper">
                                            <img class="products__create__main--media--images--item--img" :src="getPhoto()">
                                        </div>
                                    </li>

                                    <!-- upload image small -->
                                    <li class="products__create__main--media--images--item">
                                        <form class="products__create__main--media--images--item--form">
                                            <label class="products__create__main--media--images--item--form--label" for="myfile">Adicionar Imagem</label>
                                            <input class="products__create__main--media--images--item--form--input" type="file" id="myfile" @change="updatePhoto">
                                        </form>
                                    </li>
                                </ul>
                            </div>
                            
                        </div>

                    </div>
                    <div class="products__create__sidebar">
                        <!-- Product Organization -->
                        <div class="card py-2 px-2 bg-white">
                            
                            <!-- Product tension -->
                        <div class="my-3">
                            <p>Tensão</p>
                            <select class="input" v-model="form.tensao">
                                <option value="110v">110v</option>
                                <option value="220v">220v</option>
                            </select>
                        </div>

                        <!-- Product brand -->
                        <div class="my-3">
                            <p>Marca</p>
                            <select class="input" v-model="form.marca">
                                <option value="Electrolux">Electrolux</option>
                                <option value="Brastemp">Brastemp</option>
                                <option value="Fischer">Fischer</option>
                                <option value="Samsung">Samsung</option>
                                <option value="LG">LG</option>
                            </select>
                        </div>
                        </div>

                    </div>
                </div>
                <!-- Footer Bar -->
                <div class="dflex justify-content-between align-items-center my-3">
                    <p ></p>
                    <button class="btn btn-secondary" @click="updateProduct()">Save</button>
                </div>
            
        </div>
    </div>
</template>