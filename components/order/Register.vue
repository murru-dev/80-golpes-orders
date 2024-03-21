<script lang="ts" setup>
import { z } from 'zod'

const emits = defineEmits(["close"])
const loading = ref<boolean>(false)
const registerSchema = z.object({
  name: z.string()
    .min(5, { message: "Debe tener al menos 5 caracteres" })
    .max(50, { message: "Debe tener menos de 50 caracteres" })
    .regex(/^[a-zA-ZÀ-ÿ'\u00f1\u00d1,.'-]+(\s*[a-zA-ZÀ-ÿ'\u00f1\u00d1,.'-]*)*[a-zA-ZÀ-ÿ\u00f1\u00d1',.'-]+$/, { message: "Solo letras" })
    .trim(),
  address: z.string()
  .min(5, { message: "Debe tener al menos 5 caracteres" })
  .max(50, { message: "Debe tener menos de 50 caracteres" })
  .regex(/^[A-Za-zÀ-ÿ0-9ñ, ]+$/, { message: "Solo letras y números" })
  .trim(),
})
const registerForm = reactive({
  name: "",
  address: ""
})
type registerSchemaType = z.infer<typeof registerSchema>
const errors = ref<z.ZodFormattedError<registerSchemaType> | null>(null)

const goToStep = inject("change-step") as (value: string) => void

const handleBack = () => {
  errors.value = null
  goToStep("OrderAuth")
}

const handleNext = async () => {
  const validSchema = registerSchema.safeParse(registerForm)
  if (!validSchema.success) {
    errors.value = validSchema.error.format()
    return
  } else {
    errors.value = null
    loading.value = true
    await new Promise(resolve => setTimeout(resolve, 3000))
    goToStep("OrderPayMethod")
  }
}

const nextBtnText = computed(() => {
  return loading.value ? 'Registrando...' : 'Registrar'
})

const handleClose = () => {
  errors.value = null
  emits("close")
}
</script>
<template>
  <OrderStep title="Registro" :close-handler="handleClose">
    <template #body>
      <div class="w3-center w3-large">
        <p>Para realizar la compra debemos saber quién eres! Completa el siguiente formulario por favor</p>
      </div>
      <br>
      <!-- Complete name -->
      <p>
        <label>Dinos tu nombre:</label>
        <input
          class="w3-input w3-border w3-round-large"
          name="name"
          type="text"
          v-model="registerForm.name"
          :disabled="loading"
        />
        <div v-if="errors?.name" class="w3-text-red">
          <span v-for="(error, index) in errors?.name?._errors" :key="`name-err-${index}`" class="w3-block"><small>{{ error }}</small></span>
        </div>
      </p>
      <!-- Deliver address -->
      <p>
        <label>Dirección de entrega:</label>
        <input
          class="w3-input w3-border w3-round-large"
          name="address"
          type="text"
          v-model="registerForm.address"
          :disabled="loading"
        />
        <div v-if="errors?.address" class="w3-text-red">
          <span v-for="(error, index) in errors?.address?._errors" :key="`address-err-${index}`" class="w3-block"><small>{{ error }}</small></span>
        </div>
      </p>
    </template>
    <template #footer>
      <button
        class="w3-button w3-black w3-round-large w3-block"
        @click="handleBack"
        :disabled="loading"
      >
        Volver
      </button>
      <button
        class="w3-button w3-black w3-round-large w3-block"
        @click="handleNext"
        :disabled="loading"
      >
        {{ nextBtnText }}
      </button>
    </template>
  </OrderStep>
</template>
