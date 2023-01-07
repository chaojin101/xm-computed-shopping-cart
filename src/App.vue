<script setup lang="ts">
import { ref, computed } from "vue";
type Item = {
	name: string;
	num: number;
	price: number;
};
const data = ref<Item[]>([
	{
		name: "小满的裤子",
		num: 1,
		price: 100,
	},
	{
		name: "小满的衣服",
		num: 1,
		price: 200,
	},
	{
		name: "小满的丝袜",
		num: 1,
		price: 300,
	},
]);

const total_price = computed(() => {
	return data.value.reduce((pre, cur) => {
		return pre + cur.num * cur.price;
	}, 0);
});

const add_or_sub = (item: Item, type: boolean) => {
	if (item.num > 1 && !type) {
		item.num--;
	} else if (item.num < 99 && type) {
		item.num++;
	}
};

const del_data = (i: number) => data.value.splice(i, 1);
</script>

<template>
	<div>
		<table>
			<thead>
				<tr>
					<th>名称</th>
					<th>数量</th>
					<th>单价</th>
					<th>操作</th>
				</tr>
			</thead>
			<tbody>
				<tr :key="i" v-for="(item, i) in data">
					<td>{{ item.name }}</td>
					<td>
						<button @click="add_or_sub(item, false)">-</button>{{ item.num
						}}<button @click="add_or_sub(item, true)">+</button>
					</td>
					<td>{{ item.price }}</td>
					<td><button @click="del_data(i)">删除</button></td>
				</tr>
			</tbody>
			<tfoot>
				<td></td>
				<td></td>
				<td></td>
				<td>总价：{{ total_price }}</td>
			</tfoot>
		</table>
	</div>
</template>

<style scoped>
table {
	text-align: center;
	width: 100%;
}

table,
th,
td {
	border: 1px solid #ccc;
}

button {
	padding: 2px;
	margin: 2px;
}
</style>
