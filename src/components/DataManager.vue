<template>
    <div>
        <div class="app">
            <div class="apper1">
                <el-input placeholder="请输入日期" type="date" v-model="abj.date"></el-input>
            </div>
            <div class="apper2">
                <el-input placeholder="请输入姓名" v-model="abj.name"></el-input>
            </div>
            <div class="apper3">
                <el-input placeholder="请输入地址" v-model="abj.address"></el-input>
            </div>
            <el-button type="primary" @click="add()">增加</el-button>
        </div>

        <el-table ref="singleTable" :data="tableData" highlight-current-row @current-change="handleCurrentChange"
            style="width: 100%">
            <el-table-column type="index" width="50">
            </el-table-column>
            <el-table-column property="date" label="日期" width="120">
            </el-table-column>
            <el-table-column property="name" label="姓名" width="120">
            </el-table-column>
            <el-table-column property="address" label="地址">


            </el-table-column>
            <el-table-column>
                <!-- eslint-disable-next-line -->
                <template slot-scope="scope">
                    <el-button type="primary" size="small" @click="del(scope.$index)">删除</el-button>
                    <el-button type="danger" size="small" @click="edit(scope.$index, scope.row)">编辑</el-button>
                    <el-dialog title="地址" :visible.sync="dialogFormVisible">
                        <el-form :model="form">
                            <el-form-item label="日期" :label-width="formLabelWidth">
                                <el-input v-model="form.date" autocomplete="off" type="date"></el-input>
                            </el-form-item>
                            <el-form-item label="姓名" :label-width="formLabelWidth">
                                <el-input v-model="form.name" autocomplete="off"></el-input>
                            </el-form-item>
                            <el-form-item label="地址" :label-width="formLabelWidth">
                                <el-input v-model="form.address" autocomplete="off"></el-input>
                            </el-form-item>
                        </el-form>


                        <div slot="footer" class="dialog-footer">
                            <el-button @click="dialogFormVisible = false">取 消</el-button>
                            <el-button type="primary" @click="dir()">确 定</el-button>
                        </div>

                    </el-dialog>
                </template>
            </el-table-column>
        </el-table>

    </div>
</template>
 
<script>

export default {

    data() {
        return {

            editIndex: "",
            dialogTableVisible: false,
            dialogFormVisible: false,
            abj: {
                date: '',
                name: '',
                address: ''
            },
            erity: {
                date: '',
                name: '',
                address: ''
            },
            form: {
                date: '',
                name: '',
                address: '',

            },
            formLabelWidth: '120px',
            tableData: [{
                date: '2023-10-19',
                name: '马新凯',
                address: '芒果TV',
            }],
        }
    },

    methods: {

        setCurrent(row) {
            this.$refs.singleTable.setCurrentRow(row);

        },
        handleCurrentChange(val) {
            this.currentRow = val;

        },
        add() {
            this.tableData.push({
                date: this.abj.date,
                name: this.abj.name,
                address: this.abj.address,
            }),
                this.abj = {}
        },
        del(index) {
            this.tableData.splice(index, 1)
        },
        edit(index, row) {
            this.dialogFormVisible = true
            this.form = {
                date: row.date,
                name: row.name,
                address: row.address,
            }
            this.editIndex = index
        },
        dir() {
            this.tableData.splice(this.editIndex, 1, this.form)
            console.log(this.tableData[this.editIndex])
            this.dialogFormVisible = false;
        }
    }
}

</script>
<style lang="less" scoped>
.app {
    display: flex;
    justify-content: center;
    /* 在水平方向上居中 */
    align-items: center;
    /* 在垂直方向上居中 */

    .apper1 {
        width: 170px;
        padding: 0 10px;
    }

    .apper2 {
        width: 170px;
        padding: 0 10px;
    }

    .apper3 {
        width: 170px;
        padding: 0 10px;
    }
}
</style>