<script>
export default {
	props: {
		contact: { type: Object, required: true },
	},
};
</script>

<template>
	<div>
		<div class="p-1">
			<strong>Tên thức uống:</strong>
			{{ contact.namedrink }}
		</div>
		<div class="p-1">
			<strong>Size:</strong>
			{{ contact.size }}
		</div>
		<div class="p-1">
			<strong>số lượng:</strong>
			{{ contact.quantity }}
		</div>
		<div class="p-1">
			<strong>Ngày xuất hoá đơn:</strong>
			{{ contact.dateOutput }}
		</div>
		<div class="p-1">
			<strong>Thành tiền:</strong>
			{{ contact.money }}
		</div>
		<div class="p-1">
			<strong>Đã thanh toán:&nbsp;</strong>
			<i v-if="contact.favorite" class="fas fa-check"></i>
			<i v-else class="fas fa-times"></i>
		</div>
	</div>
</template>
