<script lang="ts" setup>
import { z } from "zod"

/* Define emits */
const emits = defineEmits(["close"])

/* Define validation and form features */
const authSchema = z.object({
  email: z
    .string()
    .max(50, { message: "No puede tener más de 50 caracteres" })
    .email({ message: "Formato inválido" })
    .trim()
    .toLowerCase(),
})
const loading = ref<boolean>(false)
const nextBtnText = computed(() => {
  return loading.value ? 'Verificando...' : 'Verificar'
})
const form = ref({ email: "" })
type authSchemaType = z.infer<typeof authSchema>
const errors = ref<z.ZodFormattedError<authSchemaType> | null>(null)

const goToStep = inject("change-step") as (value: string) => void
const handleNext = async () => {
  const validSchema = authSchema.safeParse(form.value)
  if (!validSchema.success) {
    errors.value = validSchema.error.format()
    return
  } else {
    errors.value = null
    loading.value = true
    await new Promise(resolve => setTimeout(resolve, 3000))
  if (form.value.email === 'ernesto@gmail.com') {
    goToStep("OrderPayMethod")
  } else {
    goToStep("OrderRegister")
  }
  }
}

const handleClose = () => {
  errors.value = null
  emits("close")
};
</script>
<template>
  <OrderStep title="Identificación" :close-handler="handleClose">
    <template #body>
      <p>
        <label>Ingresa tu correo electrónico:</label>
        <input
          class="w3-input w3-border w3-round-large"
          name="email"
          type="text"
          v-model="form.email"
          :disabled="loading"
        />
        <div v-if="errors?.email" class="w3-text-red">
          <span v-for="(error, index) in errors?.email?._errors" :key="`email-err-${index}`"><small>{{ error }}</small></span>
        </div>
      </p>
    </template>
    <template #footer>
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
