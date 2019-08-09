<template>
    <div class="attributeconfig">
        <div class="head">
<!--            <div>-->
<!--          <span style="margin-top:6px;margin-left:15px">Attribute ID :</span>-->
<!--         <Input v-model="AttributeID" placeholder="Attribute ID" style="width: 150px;height:30px" />-->
<!--      </div>-->
            <div>
                <span style="margin-top:6px;margin-left:15px">Attribute name :</span>
                <Input v-model="AttributeName" placeholder="Attribute name" style="width: 150px;height:30px" />
            </div>
<!--      <div style="display:flex;justify-content: space-between;">-->
<!--          <span style="margin-top:6px;margin-left:15px">Category :</span>-->
<!--         <i-form :model="formItem" style="width:150px;height:32px">-->
<!--                    <Form-item>-->
<!--                        <MultilevelSelect :list="cascaderList" @on-change="changeCategory" @load-data="loadSecond" ></MultilevelSelect>-->
<!--                    </Form-item>-->
<!--                </i-form>-->
<!--    </div>-->
            <div>
                <Button class="chinavasion_btn" @click="filter">Filter</Button>
            </div>
        </div>
        <div class="body">
            <div class="add">
                <Button class="chinavasion_btn" @click="showAddModel">Add</Button>
            </div>
              <Table :loading='loading' border ref="selection" :columns="columns4" :data="data1">
                  <template slot-scope="{ row, index }" slot="attr_value">
                      <div>
                          <Tag v-for="item in row.attr_value" :key="item" :name="item" @on-close="handleClose2">{{item}}</Tag>

                      </div>
                  </template>

                  <template slot-scope="{ row, index }" slot="language">
                      <div>
                          {{row.language === 0 ? 'English' : ''}}
                      </div>
                  </template>

                  <template slot-scope="{ row, index }" slot="memo">
                      <div>
                          {{row.memo}}
                      </div>
                  </template>

                   <template slot-scope="{ row, index }" slot="operation">
                    <div>

                        <Button  class="chinavasion_btn_opp" @click="Edit(row)">Edit</Button>
                        <Button  class="chinavasion_btn_opp" @click="del(row)">Delete</Button>
                    </div>
                </template>
              </Table>
                <Page style="position:fixed;right:100px;bottom:50px" :total="page.total" :page-size='page.size' show-elevator :current='page.page' @on-change='changePage'></Page>
        </div>
        <Modal v-model="ModalIf"  @on-cancel="cancelAddModel" class-name="vertical-center-modal">
            <div slot="header" class="model_header">
                <span>Attribute Recommended value config</span>

            </div>
            <div class="addForm">
                <Form  label-position="right" :label-width="100" onsubmit="return false;">
                    <FormItem label="Name :">
                        <p>{{editForm.name}}</p>

                    </FormItem>
                    <FormItem label="Language:" class="content-area">
                        <Select v-model="addForm.language" style="width:200px" placeholder="Please select" disabled>
                            <Option v-for="item in languageList" :value="item.value" :key="item.value">{{ item.label }}</Option>
                        </Select>

                    </FormItem>
                    <FormItem label="Value :" style="width: 300px;" class="input-class">
                        <!--                        <Input v-model="addForm.value" placeholder="Description for cancel"></Input>-->
                        <Tag v-for="item in editForm.value" :key="item" :name="item" closable @on-close="handleClose2">{{item}}</Tag>
<!--                        <Button icon="ios-add" type="dashed" size="small" @click="handleAdd">添加标签</Button>-->
                        <input placeholder="" @change="handleEdit($event)" v-model="tag"></input>
                    </FormItem>
                    <FormItem label="Memo :" class="content-area">
                        <Input v-model="editForm.memo" type="textarea" :rows="4" placeholder="Enter something..." />
                    </FormItem>
                </Form>
            </div>
            <div slot="footer" class="model_footer">
                <Button @click="save" class="chinavasion_btn">Submit</Button><Button @click="hide">Cancel</Button>
            </div>
        </Modal>
<!--        <Modal v-model="ModalIf" class-name="vertical-center-modal"  width="50%">-->
<!--      <p slot="header" style="text-align:center">-->
<!--        <span>Attribute Recommended value config</span>-->
<!--      </p>-->
<!--            <div class="addForm">-->
<!--                <Form :model="addForm" label-position="right" :label-width="120">-->
<!--                    <FormItem label="Attribute name：">-->
<!--                        <p>{{savedRow.attr_name}}</p>-->

<!--                    </FormItem>-->
<!--                    <FormItem label="Language：:" class="content-area">-->
<!--                        <p style="margin:30px 0">{{savedRow.language}}</p>-->

<!--                    </FormItem>-->
<!--                    <FormItem label="Value :" style="width: 300px;min-height: 80px;">-->
<!--                        &lt;!&ndash;                        <Input v-model="addForm.value" placeholder="Description for cancel"></Input>&ndash;&gt;-->
<!--                        <Tag v-for="item in addForm.value" :key="item" :name="item" closable @on-close="handleClose2">标签{{ item + 1 }}</Tag>-->
<!--                        <Button icon="ios-add" type="dashed" size="small" @click="handleAdd">添加标签</Button>-->
<!--                    </FormItem>-->
<!--                    <FormItem label="Memo :" class="content-area">-->
<!--                        <Input v-model="addForm.memo" type="textarea" :rows="4" placeholder="Enter something..." />-->
<!--                    </FormItem>-->
<!--                </Form>-->
<!--            </div>-->
<!--&lt;!&ndash;            <Form>&ndash;&gt;-->
<!--&lt;!&ndash;                <div style="width:60%;margin:30px auto">&ndash;&gt;-->
<!--&lt;!&ndash;                    <p>Attribute name：{{savedRow.attr_name}}</p>&ndash;&gt;-->
<!--&lt;!&ndash;                    <p style="margin:30px 0">language：{{savedRow.language}}</p>&ndash;&gt;-->
<!--&lt;!&ndash;                    <span>Recommended value：</span>   <Tag v-for="item in addForm.value" :key="item" :name="item" closable @on-close="handleClose2">标签{{ item + 1 }}</Tag>&ndash;&gt;-->
<!--&lt;!&ndash;                    <Button icon="ios-add" type="dashed" size="small" @click="handleAdd">添加标签</Button>&ndash;&gt;-->
<!--&lt;!&ndash;                </div>&ndash;&gt;-->

<!--&lt;!&ndash;                <FormItem label="Memo :" class="content-area">&ndash;&gt;-->
<!--&lt;!&ndash;                    <Input v-model="addForm.memo" type="textarea" :rows="4" placeholder="Enter something..." />&ndash;&gt;-->
<!--&lt;!&ndash;                </FormItem>&ndash;&gt;-->
<!--&lt;!&ndash;            </Form>&ndash;&gt;-->

<!--&lt;!&ndash;       <div></div>&ndash;&gt;-->
<!--      <div slot="footer" style="text-align:center">-->
<!--        <Button class="chinavasion_btn" @click="save">Submit</Button>-->
<!--        <Button class="chinavasion_btn_opp" @click="hide">Cancel</Button>-->
<!--      </div>-->
<!--    </Modal>-->
        <Modal v-model="showDeleteModel" class-name="vertical-center-modal" style="text-align:center" width="30%">
            <p slot="header" style="text-align:center">
                <span>Delete Attribute</span>
            </p>
            <div class="modelContent">
                Are you sure that you want to delete this attribute  ?

            </div>
            <div slot="footer" style="text-align:center">
                <Button class="chinavasion_btn" @click="submitDelete">Submit</Button>
                <Button class="chinavasion_btn_opp" @click="hide">Cancel</Button>
            </div>
        </Modal>
        <Modal v-model="showAdd"  @on-cancel="cancelAddModel" class-name="vertical-center-modal">
            <div slot="header" class="model_header">
                Add Attribute
            </div>
            <div class="addForm">
                <Form :model="addForm" label-position="right" :label-width="100">
                    <FormItem label="Name :">
                        <Input v-model="addForm.name" placeholder="name"></Input>

                    </FormItem>
                    <FormItem label="Language:" class="content-area">
<!--                        <Input v-model="addForm.language" placeholder="language" disabled></Input>-->

                                                <Select v-model="addForm.language" style="width:200px" placeholder="Please select" disabled>
                                                    <Option v-for="item in languageList" :value="item.value" :key="item.value">{{ item.label }}</Option>
                                                </Select>
                    </FormItem>
                    <FormItem label="Value :" style="width: 300px;" class="input-class">
                        <!--                        <Input v-model="addForm.value" placeholder="Description for cancel"></Input>-->
                        <Tag v-for="item in addForm.value" :key="item" :name="item" closable @on-close="handleClose">{{item}}</Tag>
                        <!--                        <Button icon="ios-add" type="dashed" size="small" @click="handleAdd">添加标签</Button>-->
                        <input placeholder="" @change="handleAdd($event)" v-model="tag"></input>
                    </FormItem>
                    <FormItem label="Memo :" class="content-area">
                        <Input v-model="addForm.memo" type="textarea" :rows="4" placeholder="Enter something..." />
                    </FormItem>
                </Form>
            </div>
            <div slot="footer" class="model_footer">
                <Button @click="submitAddModel" class="chinavasion_btn">Submit</Button><Button @click="cancelAddModel">Cancel</Button>
            </div>
        </Modal>

    </div>
</template>

<script>
import MultilevelSelect from '../../components/MultilevelSelect'
export default {
    data(){
        return{
            formItem:{
                select:"",
            },
            AttributeID:'',
            AttributeName:'',
            ModalIf:false,
            RecommendedValue:"",
            loading:false,
             page: {
                total: 0,
                size: 5,
                page: 1,
            },
            columns4: [
                   
                    // {
                    //     title: 'Attribute ID',
                    //     key: 'attr_id',
                    //     align:'center'
                    // },
                    {
                        title: 'Attribute name',
                        key: 'attr_name',
                         align:'center'
                    },
                    {
                        title: 'Recommended value',
                        key: 'attr_value',
                         align:'center',
                        slot: 'attr_value'
                    },
                    {
                        title:'Language',
                        key:'language',
                        slot: 'language',
                        align:'center'
                    },
                    {
                        title:'Memo',
                        slot: 'memo',
                        key:'mome',
                        align:'center'
                    },
                    {
                    title: 'Operation',
                    slot: 'operation',
                    width: 180,
                    align: 'center',
                },
                ],
                data1: [
                   
                ],
                savedRow: '',
            cascaderList: [],
            categoryId: '',
            showDeleteModel: false,
            showAdd: false,
            addForm: {
                name: '',
                language: '0',
                value: [],
                memo: ''
            },
            editForm: {
                name: '',
                language: '0',
                value: [],
                memo: '',
                attr_id: ''
            },
            cancelModelFlag: false,
            languageList: [
                {
                    label: 'English',
                    value: '0'
                }
            ],
            tag: ''
        }
    },
    components: {
        MultilevelSelect
    },
    methods:{
        //修改
        Edit(row){
            console.log(row)
            this.ModalIf = true;
            this.editForm.attr_id = row.attr_id
            this.editForm.name = row.attr_name
            this.editForm.language = row.language === 0 ? row.language : ''
            this.editForm.value = [...row.attr_value]
            this.editForm.memo = row.memo
        },
        //弹出模态框
        save(){
            let param = {
                attr_id: this.editForm.attr_id,
                language: this.editForm.language,
                name: this.editForm.name,
                memo: this.editForm.memo,
                value: this.editForm.value.join(',')
            }
            console.log(param)
            if (this.editForm.name === '' || this.editForm.language === '' || this.editForm.value.length === 0 || this.editForm.memo === '') {
                this.$Message.warning('Form item can\'t be empty')
                return false
            }
            console.log(param)

            this.$axios.put(`${this.$BaseURL}/category/add_cate_attr`,param).then((response) => {
                console.log(response)
                if (response.data.code === 10000) {
                    this.$Message.success('Modefied successfully');
                    this.ModalIf = false
                    this.tag = ''
                    this.getdata()
                }
            }).catch((err) => {
                console.log(err)
            })
        },
        del (item) {
            this.showDeleteModel = true
            this.savedRow = item
        },
        submitDelete(){
            this.$axios({
                method: 'DELETE',
                url: `${this.$BaseURL}/category/attribute`,
                data:{
                    attribute_id: this.savedRow.attr_id,
                }

            }).then(res => {

                if (res.data.code==10000) {
                    this.$Message.success({
                        content: res.data.msg,
                        duration: 3,
                        closable: true
                    });
                this.getdata()
                this.showDeleteModel = false

                } else {
                    this.$Message.error({
                        content: res.data.msg,
                        duration: 3,
                        closable: true
                    });
                    this.showDeleteModel = false

                }
            }).catch(err => {
                this.$Message.error({
                    content: err.data.msg,
                    duration: 3,
                    closable: true
                });
            });
        },
        //过滤
        filter(){
            this.page.page = 1
            this.getdata()
        },
        //页面加载获取数据
        getdata () {
            //  this.loading = true;
            this.$axios({
                method: 'post',
                url: `${this.$BaseURL}/category/attribute`,
                headers: {
                    "token": window.localStorage.getItem('token')
                },
                data:{
                        attribute_name: this.AttributeName,
                        offset:(this.page.page-1)*this.page.size,
                        limit:this.page.size
                }
               
            }).then(res => {
                                   
              if (res.data.code==10000) {
                  // res.data.data.result.forEach((item) => {
                  //     item.attr_value = item.attr_value
                  // })
              this.data1 = res.data.data.result
              this.page.total = res.data.data.total
              // console.log(res.data.data[5].total)
              // console.log(this.page.total)
              this.loading = false;
              // console.log(this.data1)
                } else {
                  
                }
            }).catch(err => {
                
            });
        },
        changePage(nowpage){
            this.page.page = nowpage;
            this.getdata()
        },
        hide () {
            this.ModalIf = false
            this.showDeleteModel = false
            this.RecommendedValue = ''
            this.savedRow = ''
            this.tag = ''
        },
        // 请求一级category
        loadCategory () {
            let param = {
                category_id: ''
            }
            this.$axios.post(`${this.$BaseURL}/category/list`,param).then((response) => {
                console.log(response.data.data)
                response.data.data.children.forEach((item) => {
                    let obj = {}
                    // console.log(item)
                    // if (item.id >0 && item.id < 7) {
                    //     Reflect.set(obj,'value',item.id);
                    //     Reflect.set(obj,'label',item.name);
                    // } else {
                    //
                    // }
                    Reflect.set(obj,'value',item.id);
                    Reflect.set(obj,'label',item.name);
                    if (item.has_child === 1) {
                        Reflect.set(obj,'children',[]);

                        Reflect.set(obj,'loading',false);
                    }


                    this.cascaderList.push(obj);
                })
                // setTimeout(() => {
                //     document.querySelector('.ivu-cascader-menu').style.width = 'fit-content';
                // })
            }).catch((err) => {

            })
        },
        //请求二级category
        loadSecond (args) {
            console.log(args)
            // return false
            let param = {
                category_id: args.item.value
            }
            console.log(JSON.stringify(args.item))
            args.item.loading = true;

            this.$axios.post(`${this.$BaseURL}/category/list `,param)
                .then(response=>{
                    console.log(response);
                    if (!response.data.data.children) {
                        setTimeout(() => {
                            args.item.children = [{label: '', value: ''}]
                            args.item.loading = false;
                            args.callback();
                        },100);
                        return false
                    }
                    let arr = []

                    response.data.data.children.forEach((item) => {
                        // console.log(item)
                        let obj = {}
                        Reflect.set(obj,'value',item.id);
                        Reflect.set(obj,'label',item.name);
                        if (item.has_child === 1) {
                            Reflect.set(obj,'children',[]);

                            Reflect.set(obj,'loading',false);
                        }
                        arr.push(obj);
                    })

                    console.log(JSON.stringify(this.cascaderList))
                    setTimeout(() => {
                        args.item.children = arr
                        //  args.item.children = [{
                        //      value: 'beijing',
                        //      label: '北京'
                        //
                        //  }, {
                        //      value: 'jiangsu',
                        //      label: '江苏'
                        //  }]
                        args.item.loading = false;
                        args.callback();
                        // setTimeout(() => {
                        //     document.querySelector('.ivu-cascader-menu').style.width = 'fit-content';
                        // })
                    }, 1000);

                }).catch((err) => {
                args.item.loading = false;
            });
        },
        changeCategory (args) {
            console.log(args,args.value[0])

            this.addForm.categoryId = args.value[args.value.length -1]
            console.log(this.category)
        },
        showAddModel (item) {
            this.showAdd = true
            // this.orderInfo = item
        },
        submitAddModel () {
            if (this.addForm.name === '' || this.addForm.language === '' || this.addForm.value.length === 0 || this.addForm.memo === '') {
                this.$Message.warning('Form item can\'t be empty')
                return false
            }
            this.$axios({
                method: 'post',
                url: `${this.$BaseURL}/category/add_cate_attr`,
                headers: {
                    "token": window.localStorage.getItem('mtoken')
                },
                data:{
                    name: this.addForm.name,
                    language: this.addForm.language,
                    value: this.addForm.value.join(','),
                    memo: this.addForm.memo,
                }

            }).then(res => {

                if (res.data.code==10000) {


                    // this.page.total = res.data.data
                    this.loading = false;
                    this.showAdd = false
                    this.$Message.success(res.data.msg)
                    this.getdata()
                    //初始化addForm
                    this.resetAddForm()
                    // this.cancelForm.cancelReason = ''
                    // this.cancelForm.description = ''

                } else {
                    this.loading = false;
                    // console.log(res)
                    this.$Message.warning(res.data.msg);
                }
            }).catch(err => {
                this.loading = false;
                // this.cancelModelFlag = false
                this.$Message.warning(err.data.msg);

            });
        },
        cancelAddModel () {
            this.showAdd = false
            this.orderInfo = ''
            //初始化addForm
            this.resetAddForm()
            // this.cancelForm.cancelReason = ''
            // this.cancelForm.description = ''
        },
        resetAddForm () {
            this.addForm.name = ''
            this.addForm.language = '0'
            this.addForm.value = []
            this.addForm.memo = ''
        },
        handleEdit (event) {
            console.log(event)
            if (!event.target.value) {
                return false
            }
            if (this.editForm.value.includes(event.target.value)){
                this.$Message.warning('This tag has been added')
                return false
            }

            this.editForm.value.push(event.target.value);
            this.tag = ''
        },
        handleClose2 (event, name) {
            const index = this.editForm.value.indexOf(name);
            this.editForm.value.splice(index, 1);
        },
        handleAdd (event) {
            console.log(event)
            if (!event.target.value) {
                return false
            }
            if (this.addForm.value.includes(event.target.value)){
                this.$Message.warning('This tag has been added')
                return false
            }

            this.addForm.value.push(event.target.value);
            this.tag = ''
        },
        handleClose (event, name) {
            const index = this.addForm.value.indexOf(name);
            this.addForm.value.splice(index, 1);
        }
    },
    mounted(){
        this.getdata()
        this.loadCategory()
    }
}
</script>

<style lang="scss" scoped>
.attributeconfig{
    width: 90%;
    margin: 30px auto;
    .head{
        width: 80%;
        height: 40px;
        display: flex;
        /*justify-content: space-around;*/
        align-items: center;
        &>div{
            margin-right: 30px;
        }
    }
    .body{
        width: 100%;
        margin: 30px 0;
    }
}
    .add{
        margin: 10px 0;
        display: flex;
        justify-content: flex-end;
    }
.vertical-center-modal{
    display: flex;
    align-items: center;
    justify-content: center;

    .ivu-modal{
        top: 0;
    }
}
.model_footer{
    display: flex;
    justify-content: center;
    align-items: center;
    button{
        margin: 0 30px;
        width: 100px;
    }
}
    .model_header{
        display: flex;
        justify-content: center;
    }
.addForm{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 500px;
    /*height: 200px;*/
    /*width: 80%;*/
    p{
        width: 80%;
    }
}
    .input-class{
        input{
            width: 50px;
            height: 20px;
            display: inline-block;
            height: 22px;
            line-height: 22px;
            margin: 2px 4px 2px 0;
            padding: 0 8px;
            border: 1px solid #e8eaec;
            border-radius: 3px;
            font-size: 12px;
            vertical-align: middle;
            opacity: 1;
            overflow: hidden;
            cursor: pointer;
        }
    }
</style>
<style scoped>
    .ivu-cascader-menu{
        width: fit-content;
    }
</style>


