<template>
	<div class="yj-demo-wrap">
		<el-table
    :data="goodInfo"
    stripe
    style="width: 100%">
		<el-table-column type="expand">
      <template slot-scope="props">
        <el-form label-position="left" inline class="demo-table-expand">
          <el-form-item label="商品名称">
            <span>{{ props.row.name }}</span>
          </el-form-item>
          <el-form-item label="月售">
            <span v-show="props.row.count">{{ props.row.count }}件</span>
          </el-form-item>
          <el-form-item label="原价">
            <span v-show="props.row.oldPrice">¥{{ props.row.oldPrice }}</span>
          </el-form-item>
          <el-form-item label="惊爆价">
            <span v-show="props.row.newPrice">¥{{ props.row.newPrice }}</span>
          </el-form-item>
          <el-form-item label="排序">
            <span>{{ props.row.sort }}</span>
          </el-form-item>
          <el-form-item label="描述">
            <span>{{ props.row.desc }}</span>
          </el-form-item>
        </el-form>
      </template>
    </el-table-column>
    <el-table-column
      prop="name"
      label="商品名称"
      width="180">
    </el-table-column>
    <el-table-column
      prop="count"
      label="月售"
      width="180">
    </el-table-column>
    <el-table-column
      prop="oldPrice"
      label="原价"
      width="180">
    </el-table-column>
    <el-table-column
      prop="newPrice"
      label="惊爆价"
      width="180">
    </el-table-column>
    <el-table-column
      prop="sort"
      label="排序"
      width="180">
    </el-table-column>
		<el-table-column
      fixed="right"
      label="操作"
      width="220">
			<template slot="header">
        <el-button @click="add()" size="small">添加</el-button>
      </template>
      <template slot-scope="scope">
        <el-button @click="edit(scope.row, scope.$index)" type="text" size="small">修 改</el-button>
        <el-button @click="del(scope.$index)" type="text" size="small">删 除</el-button>
      </template>
    </el-table-column>
  </el-table>

		<el-dialog
			title="添加商品"
			width="80%"
			:visible.sync="addShow">
					<el-form :label-position="'right'" label-width="80px" :model="product">
					<el-form-item label="名称">
						<el-input v-model="product.name"></el-input>
					</el-form-item>
					<el-form-item label="描述">
						<el-input v-model="product.desc"></el-input>
					</el-form-item>
					<el-form-item label="月售">
						<el-input v-model="product.count"></el-input>
					</el-form-item>
					<el-form-item label="现价">
						<el-input v-model="product.newPrice"></el-input>
					</el-form-item>
					<el-form-item label="原价">
						<el-input v-model="product.oldPrice"></el-input>
					</el-form-item>
					<el-form-item label="排序">
						<el-input v-model="product.sort"></el-input>
					</el-form-item>
				</el-form>
			<span slot="footer" class="dialog-footer">
				<el-button @click="addShow = false">取 消</el-button>
				<el-button type="primary" @click="submitForm">{{ addText }}</el-button>
			</span>
		</el-dialog>
	</div>
</template>

<script>
const PRODUCT_SORT = 100;
export default {

	data() {
		return {
			goodInfo: [],
			goodInfoIndex: -1,
			product: {
				name: '',
				desc: '',
				count: '',
				newPrice: '',
				oldPrice: '',
				sort: PRODUCT_SORT
			},
			addText: '保 存',
			addShow: false
		}
	},
	methods: {
		add() {
			this.product = {};
			this.product.sort = PRODUCT_SORT;
			this.addText = '保 存';
			this.goodInfoIndex = -1;
			this.addShow = true;
		},
		edit(good, index) {
			this.addText = '修 改';
			this.product = good;
			this.goodInfoIndex = index;
			this.addShow = true;
		},
		del(index) {
			this.goodInfo.splice(index, 1);
		},
		submitForm() {
			let product = {};
			product = JSON.parse(JSON.stringify(this.product));
			if(this.goodInfoIndex === -1) { //添加
				this.goodInfo.push(product);
			} else { //修改
				this.goodInfo[this.goodInfoIndex] = product;
			}
			this.addShow = false;
		},
	},
}
</script>

<style lang="scss">
.demo-table-expand {
	font-size: 0;
	label {
		width: 90px;
		color: #99a9bf;
	}
	.el-form-item {
		margin-right: 0;
		margin-bottom: 0;
		width: 50%;
	}
}
</style>

