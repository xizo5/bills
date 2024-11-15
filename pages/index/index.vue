<template>
	<view class="content">
		<!-- 本月账单 -->
		<view class="bill">
			<!-- 	<view class="bill_title">
				本月账单
			</view> -->
			<view class="bill_content">
				<view class="bill_content_item">
					<view class="bill_content_item_title">收入</view>
					<view class="bill_content_item_price">￥0</view>
				</view>
				<view class="bill_content_item">
					<view class="bill_content_item_title">支出</view>
					<view class="bill_content_item_price">￥0</view>
				</view>
			</view>

		</view>
		<!-- 账单列表 -->
		<view class="u-p-50">
			<up-empty v-if="billsList.length==0" />
			<view v-else>
				<view v-for="item in billsList">
					<view class="">
						时间：{{item.time}}
					</view>
					<view class="">
						金额: {{item.price}}
					</view>
					<view class="">
						备注: {{item.remark}}
					</view>
				</view>
			</view>
		</view>
		<up-popup :show="show" closeable @close="close">
			<up-form labelPosition="top" :model="formData" :rules="rules" ref="form1" class="form">
				<up-form-item label="标签" prop="tags" required>
					<up-checkbox-group v-model="formData.tags">
						<up-checkbox :customStyle="{marginRight: '20rpx'}" v-for="(item, index) in checkboxList1"
							:key="index" :label="item.name" :name="item.name">
						</up-checkbox>
					</up-checkbox-group>
				</up-form-item>
				<up-form-item label="金额" prop="price" required>
					<up-input v-model="formData.price" placeholder="请输入本次需要记录的金额"></up-input>
				</up-form-item>
				<up-form-item label="备注">
					<up-input v-model="formData.remark" placeholder="如果有备注请在此输入"></up-input>
				</up-form-item>
			</up-form>
			<view class="sub_btn" @click="submit">添加</view>
		</up-popup>

		<view class="add_bills_btn" @click="addBills">
			记一笔
		</view>
	</view>
</template>

<script>
	import dayjs from 'dayjs';
	export default {
		data() {
			return {
				billsList: [],
				formData: {
					price: '',
					tags: '',
					remark: '',
				},
				checkboxList1: [{
						name: '餐饮饮食',
						disabled: false,
					},
					{
						name: '零食饮料',
						disabled: false,
					},
					{
						name: '烟酒槟榔',
						disabled: true,
					},
				],
				rules: {
					tags: [{
						required: true,
						message: '最少选择一个标签',
						type: 'array',
						trigger: 'change',
						min: 1,

					}],
					price: [{
						required: true,
						message: '请输入金额',
						trigger: 'blur',
					}],
				},
				show: false,
				title: 'Hello'
			}
		},

		methods: {
			async submit() {
				console.log('表单值', this.formData);


				let validate = await this.$refs.form1.validate()
				if (!validate) return

				let time = dayjs()
					.format("YYYY-MM-DD HH:mm:ss");

				this.billsList.push({
					time,
					...this.formData
				})
			},
			addBills() {
				this.show = true;
				console.log('添加账单');
			},
			close() {
				this.show = false;
			},

		}
	}
</script>

<style lang="scss" scoped>
	.content {
		height: 100vh;
		// background-color: #c4dcff;
		position: relative;
		padding: 1px;
	}

	.bill {
		.bill_title {
			font-size: 40rpx;
			font-weight: bold;
			color: #007AFF;
			text-align: center;
		}

		.bill_content {
			display: flex;
			justify-content: space-between;
			margin-top: 30rpx;

			.bill_content_item {
				width: 100%;
				text-align: center;
			}
		}
	}





	.form {
		padding: 60rpx;
	}

	.sub_btn {
		width: 100%;
		height: 100rpx;
		background-color: #007AFF;
		color: white;
		text-align: center;
		line-height: 100rpx;

	}

	.add_bills_btn {
		height: 100rpx;
		width: 100rpx;
		text-align: center;
		color: white;
		font-size: 20rpx;
		line-height: 100rpx;
		border-radius: 50%;
		background-color: #007AFF;
		position: fixed;
		bottom: 150rpx;
		right: 80rpx;

		&:active {
			background-color: gray;
		}
	}
</style>