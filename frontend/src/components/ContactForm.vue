<template>
	<Form
		ref="contactForm"
		@submit="submitContact"
		:validation-schema="contactFormSchema"
	>
		<div class="form-group">
			<label for="namedrink">Tên đồ uống</label>
			<Field
				name="namedrink"
				type="text"
				class="form-control"
				v-model="contactLocal.namedrink"
			/>
			<ErrorMessage name="namedrink" class="error-feedback" />
		</div>
		<div class="form-group">
			<label for="size">Size</label>
			<Field
				name="size"
				type="text"
				class="form-control"
				v-model="contactLocal.size"
			/>
			<ErrorMessage name="size" class="error-feedback" />
		</div>
		<div class="form-group">
			<label for="quantity">Số lượng</label>
			<Field
				name="quantity"
				type="text"
				class="form-control"
				v-model="contactLocal.quantity"
			/>
			<ErrorMessage name="quantity" class="error-feedback" />
		</div>
		<div class="form-group">
			<label for="dateOutput">Ngày xuất hoá đơn</label>
			<Field
				name="dateOutput"
				type="text"
				class="form-control"
				v-model="contactLocal.dateOutput"
			/>
			<ErrorMessage name="dateOutput" class="error-feedback" />
		</div>

		<div class="form-group">
			<label for="money">Thành tiền</label>
			<Field
				name="money"
				type="text"
				class="form-control"
				v-model="contactLocal.money"
			/>
			<ErrorMessage name="money" class="error-feedback" />
		</div>
			
		<div class="form-group form-check">
			<input
				name="favorite"
				type="checkbox"
				class="form-check-input"
				v-model="contactLocal.favorite"
			/>
			<label for="favorite" class="form-check-label">
				<strong>Đã thanh toán</strong>
			</label>
		</div>

		<div class="form-group">
			<button class="btn btn-danger">
				<i class="fas fa-save"></i> Lưu
			</button>
			<button
				v-if="contactLocal._id"
				type="button"
				class="ml-2 btn btn-danger"
				@click="deleteContact"
			>
				<i class="fas fa-trash"></i> Xóa
			</button>
		</div>
	</Form>
</template>

<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";

export default {
	components: {
		Form,
		Field,
		ErrorMessage,
	},
	emits: ["submit:contact", "delete:contact"],
	props: {
		contact: { type: Object, required: true },
		resetAfterSubmit: { type: Boolean, default: false },
	},
	data() {
		const contactFormSchema = yup.object().shape({
			namedrink: yup
				.string()
				.required("Tên đồ uống phải có tên.")
				.min(2, "Tên đồ uống phải ít nhất 2 ký tự.")
				.max(50, "Tên đồ uống có nhiều nhất 50 ký tự."),
			size: yup
				.string()
				.max(5, "size tối đa 5 ký tự."),
			quantity: yup.string().max(100, "Số lượng tối đa 100 ký tự."),
			dateOutput: yup
				.string()
				.min(7,"Ngày xuất hoá đơn ít nhất 7 kí tự")
				.max(100,"Ngày xuất hoá đơn chỉ tối đa 100 ký tự"),
			money: yup
			    .string()
				.max(12,"số tiền có thể nhập tối đa 12 ký tự"),
		});
		return {
			contactLocal: this.contact,
			contactFormSchema,
		};
	},
	methods: {
		submitContact() {
			this.$emit("submit:contact", this.contactLocal);
			if (this.resetAfterSubmit) {
				this.$refs.contactForm.resetForm();
			}
		},
		deleteContact() {
			this.$emit("delete:contact", this.contactLocal._id);
		},
	},
};
</script>

<style scoped>
@import "@/assets/form.css";
</style>
