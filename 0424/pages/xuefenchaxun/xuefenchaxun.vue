<template>
    <view class="warp">
        <view class="box">
			<view class="chaxunlianjie">
				<input  class="text1" focus="true" style="border: #007AFF 2rpx solid;" v-model="chaxunzhi" placeholder="请输入查询年份"/>
				 <button @click="chaxun">查询</button>
			</view>
            <t-table>
                <t-tr>
                    <!-- <t-th>
						<picker @change="bindPickerChange" :value="index" :range="array">
						    <view class="uni-input">{{array[index]}}</view>
						</picker>
					</t-th> -->
					<t-th>序号</t-th>
                    <t-th>活动名称</t-th>
                    <t-th>所得学分</t-th>
                    <t-th>时间</t-th>
                </t-tr>
                <t-tr v-for="(item,index) in tableList" :key="index">
				<!-- <t-tr v-for="(item,index) in tableList"> 
				不要key也可以运行 -->
                    <t-td>{{ index+1 }}</t-td>
                    <t-td>{{ item.noticeCode }}</t-td>
                    <t-td>{{ item.rCredit }}</t-td>
                    <t-td>{{ item.recordYear }}</t-td>
					
                </t-tr>
            </t-table>
        </view>
    </view>
</template>
<script>
	
	    import tTable from '@/components/t-table/t-table.vue';
	    import tTh from '@/components/t-table/t-th.vue';
	    import tTr from '@/components/t-table/t-tr.vue';
	    import tTd from '@/components/t-table/t-td.vue';
	    export default {
	        components: {
	            tTable,
	            tTh,
	            tTr,
	            tTd
	        },
			data() {
			    return {
					chaxunzhi:'',
					index: 0,
					tableList:[]
			    };
			},
	        methods: {
				chaxun:function(){	
					var that=this;
					uni.request({
						url:"http://192.168.1.143:8080/RecordCredit/getByRecordYear",
						method:"POST",
						header: {
							'content-type': 'application/x-www-form-urlencoded', 
						},
						data:{recordYear:that.chaxunzhi},
						success:function(res){
							console.log(res);
							that.tableList=res.data.data;
							console.log(that.tableList);
							}
					})
				}
				
	        }
	    }
</script>

<style>
	.title{ text-align: right;}
	.chaxunlianjie{display: flex; width: 94% ;padding: 10upx 3%;}
	.chaxunlianjie button{ height: ;}
	.text1{margin: 20rpx;height:auto;}
</style>