<template>
  <div class="hd">
    <div class="hd-section flex-center-sb">
      <div class="title-w flex-center">
        <div class="title">{{contract.name}}</div>
        <div class="title-btn-item flex-center">{{contract.chain.name || contract.chain.chainName}}</div>
      </div>
      <div class="hd-btns flex-center">
        <div v-if="contract.token">
          <div v-if="!contract.isImport && contract.hasUpdate" class="hd-btn-item flex-center-center btn hd-btn-item-red" @click="updateShare">
            <img src="@/assets/images/update.svg" alt="">
            <span>Uptede</span>
          </div>
          <div v-if="contract.isImport && contract.hasSync" class="hd-btn-item flex-center-center btn hd-btn-item-red" @click="() => showHint = true">
            <img src="@/assets/images/arrow_reload.svg" alt="">
            <span>Sync</span>
          </div>
        </div>
        <div class="hd-btn-item flex-center-center btn" @click="copy(contract.abi, 'abi')">
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M10.8333 17.5L3.33333 17.5C2.8731 17.5 2.5 17.1269 2.5 16.6667L2.5 5.83333C2.5 5.3731 2.8731 5 3.33333 5L7.98816 5C8.20917 5 8.42113 5.0878 8.57741 5.24408L11.4226 8.08925C11.5789 8.24554 11.6667 8.4575 11.6667 8.67851V16.6667C11.6667 17.1269 11.2936 17.5 10.8333 17.5Z" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M8.33325 5L8.33325 3.33333C8.33325 2.8731 8.70635 2.5 9.16659 2.5L13.8214 2.5C14.0424 2.5 14.2544 2.5878 14.4107 2.74408L17.2558 5.58925C17.4121 5.74554 17.4999 5.9575 17.4999 6.17851V14.1667C17.4999 14.6269 17.1268 15 16.6666 15L11.6666 15" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M11.6667 9.16667L8.33333 9.16667C7.8731 9.16667 7.5 8.79357 7.5 8.33333L7.5 5" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M17.4999 6.66667L14.1666 6.66667C13.7063 6.66667 13.3333 6.29357 13.3333 5.83333L13.3333 2.5" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <span>Copy ABI</span>
        </div>
        <div v-if="isIframe" class="hd-btn-item flex-center-center btn " @click="copy(contract.address)">
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M10.8333 17.5L3.33333 17.5C2.8731 17.5 2.5 17.1269 2.5 16.6667L2.5 5.83333C2.5 5.3731 2.8731 5 3.33333 5L7.98816 5C8.20917 5 8.42113 5.0878 8.57741 5.24408L11.4226 8.08925C11.5789 8.24554 11.6667 8.4575 11.6667 8.67851V16.6667C11.6667 17.1269 11.2936 17.5 10.8333 17.5Z" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M8.33325 5L8.33325 3.33333C8.33325 2.8731 8.70635 2.5 9.16659 2.5L13.8214 2.5C14.0424 2.5 14.2544 2.5878 14.4107 2.74408L17.2558 5.58925C17.4121 5.74554 17.4999 5.9575 17.4999 6.17851V14.1667C17.4999 14.6269 17.1268 15 16.6666 15L11.6666 15" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M11.6667 9.16667L8.33333 9.16667C7.8731 9.16667 7.5 8.79357 7.5 8.33333L7.5 5" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M17.4999 6.66667L14.1666 6.66667C13.7063 6.66667 13.3333 6.29357 13.3333 5.83333L13.3333 2.5" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <span>Copy Address</span>
        </div>
        <div class="hd-btn-item flex-center-center hd-btn-item-h btn hover-6F4AC5" @click="getSourceCode">
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <g clip-path="url(#clip0_1151_17154)">
            <path d="M6.66669 5.41669L1.66669 10.5968L6.66669 15.4167" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M13.3333 5.41669L18.3333 10.5968L13.3333 15.4167" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M11.6667 1.66669L8.75 18.3334" stroke="#858D99" stroke-width="1.5" stroke-linecap="round"/>
            </g>
            <defs>
            <clipPath id="clip0_1151_17154">
            <rect width="20" height="20" fill="white"/>
            </clipPath>
            </defs>
          </svg>
          <span>Source Code</span>
        </div>
        <div class="hd-btn-item flex-center-center btn hd-btn-item-h hover-0670A6" @click="toEtherscanAddress(contract.address, contract.chain)">
          <img src="@/assets/images/show.svg" alt="">
          <span>View Etherscan</span>
        </div>
        <div class="hd-btn-item flex-center-center btn hd-btn-item-h hover-57B36F" @click="decode">
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M3.75 2.91663L9.58333 8.74996L3.75 14.5833" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M7.08337 17.0834H16.25" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <span>Decode Input</span>
        </div>
        <div v-if="!isIframe" class="hd-btn-item flex-center-center btn hd-btn-item-h" @click="share">
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M15 17.5C16.3807 17.5 17.5 16.3807 17.5 15C17.5 13.6193 16.3807 12.5 15 12.5C13.6193 12.5 12.5 13.6193 12.5 15C12.5 16.3807 13.6193 17.5 15 17.5Z" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M7.5 11.25L12.5 13.75" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M5 12.5C6.38071 12.5 7.5 11.3807 7.5 10C7.5 8.61929 6.38071 7.5 5 7.5C3.61929 7.5 2.5 8.61929 2.5 10C2.5 11.3807 3.61929 12.5 5 12.5Z" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M12.5 6.25L7.5 8.75" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M15 7.5C16.3807 7.5 17.5 6.38071 17.5 5C17.5 3.61929 16.3807 2.5 15 2.5C13.6193 2.5 12.5 3.61929 12.5 5C12.5 6.38071 13.6193 7.5 15 7.5Z" stroke="#858D99" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <span>Share</span>
        </div>
        <div v-if="((!contract.isImport && contract.token) || !contract.token) && !isIframe" class="hd-btn-item flex-center-center btn hd-btn-item-h" @click="edit">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M2.66663 13.3334H13.3333" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M2.66663 13.3333H5.33329L12.8619 5.80474C13.1222 5.54439 13.1222 5.12228 12.8619 4.86193L11.138 3.13807C10.8777 2.87772 10.4556 2.87772 10.1952 3.13807L2.66663 10.6667V13.3333Z" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <span>Edit</span>
        </div>
        <div v-if="!isIframe" class="hd-btn-item flex-center-center btn hd-btn-item-h hover-F43658" @click="del">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M11.6 4.40002H4.39999V12.8C4.39999 13.1314 4.66862 13.4 4.99999 13.4H11C11.3314 13.4 11.6 13.1314 11.6 12.8V4.40002Z" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M3.20001 4.40002H12.8" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M9.80001 2.59998H6.20001C5.86864 2.59998 5.60001 2.8686 5.60001 3.19998V4.39998H10.4V3.19998C10.4 2.8686 10.1314 2.59998 9.80001 2.59998Z" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <span>Delete</span>
        </div>
      </div>
    </div>
    <div class="desc">{{contract.remark}}</div>
    <div class="flex-center-sb info" v-if="!isIframe">
      <div class="flex-center">
        <div class="info-item flex-center" @click="toEtherscanAddress(contract.address, contract.chain)">
          <div class="info-key">Contract Address</div>
          <div class="info-value info-value-a">{{getAddress(contract.address)}}</div>
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg" @click.stop="copy(contract.address)">
            <path d="M8.66667 14L2.66667 14C2.29848 14 2 13.7015 2 13.3333L2 4.66667C2 4.29848 2.29848 4 2.66667 4L6.39053 4C6.56734 4 6.73691 4.07024 6.86193 4.19526L9.13807 6.4714C9.2631 6.59643 9.33334 6.766 9.33334 6.94281V13.3333C9.33334 13.7015 9.03486 14 8.66667 14Z" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M6.66666 4L6.66666 2.66667C6.66666 2.29848 6.96513 2 7.33332 2L11.0572 2C11.234 2 11.4036 2.07024 11.5286 2.19526L13.8047 4.4714C13.9298 4.59643 14 4.766 14 4.94281V11.3333C14 11.7015 13.7015 12 13.3333 12L9.33332 12" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M9.33333 7.33333L6.66667 7.33333C6.29848 7.33333 6 7.03486 6 6.66667L6 4" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M14 5.33333L11.3333 5.33333C10.9651 5.33333 10.6667 5.03486 10.6667 4.66667L10.6667 2" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </div>
        <div class="info-line" v-if="contract.contractCreator"></div>
        <div class="info-item flex-center" v-if="contract.contractCreator" @click="toEtherscanAddress(contract.contractCreator, contract.chain)">
          <div class="info-key">Creator Address</div>
          <div class="info-value info-value-a">{{getAddress(contract.contractCreator)}}</div>
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg" @click.stop="copy(contract.contractCreator)">
            <path d="M8.66667 14L2.66667 14C2.29848 14 2 13.7015 2 13.3333L2 4.66667C2 4.29848 2.29848 4 2.66667 4L6.39053 4C6.56734 4 6.73691 4.07024 6.86193 4.19526L9.13807 6.4714C9.2631 6.59643 9.33334 6.766 9.33334 6.94281V13.3333C9.33334 13.7015 9.03486 14 8.66667 14Z" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M6.66666 4L6.66666 2.66667C6.66666 2.29848 6.96513 2 7.33332 2L11.0572 2C11.234 2 11.4036 2.07024 11.5286 2.19526L13.8047 4.4714C13.9298 4.59643 14 4.766 14 4.94281V11.3333C14 11.7015 13.7015 12 13.3333 12L9.33332 12" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M9.33333 7.33333L6.66667 7.33333C6.29848 7.33333 6 7.03486 6 6.66667L6 4" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M14 5.33333L11.3333 5.33333C10.9651 5.33333 10.6667 5.03486 10.6667 4.66667L10.6667 2" stroke="#858D99" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </div>
        <div class="info-line"></div>
        <div class="info-item flex-center" >
          <div class="info-key">Contract Balance</div>
          <div class="info-value">{{balance}}</div>
        </div>
        
      </div>
      <div v-if="contract.userList && contract.userList.length" class="team flex-center">
        <p>Team Members</p>
        <div class="flex-center">
          <div class="user-list flex-center">
            <div v-for="(item, index) in contract.userList" :key="item.nickname">
              <div class="user-avatar" v-if="index < 5">
                <n-popover trigger="hover">
                  <template #trigger>
                    <Avatar :width="32" :avatar="item.avatar" :address="item.address" />
                  </template>
                  <span>{{item.nickname}}</span>
                </n-popover>
              </div>
            </div>
            <div v-if="contract.userList.length > 5" class="user-avatar">
              <div class="more flex-center-center">+{{contract.userList.length - 5}}
                <div class="more-list">
                <div v-for="(item, index) in contract.userList" :key="item.nickname">
                  <div v-if="index > 4" class="user-item flex-center">
                    <div class="item-avatar">
                      <Avatar :width="18" :avatar="item.avatar" :address="item.address" />
                    </div>
                    <span>{{item.nickname}}</span>
                  </div>
                </div>
              </div>
              </div>
            </div>
          </div>
          <div class="team-edit" @click="showTeamModal">
            <!-- <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M2.6665 13.3334H5.33317L12.8618 5.8048C13.1221 5.54445 13.1221 5.12234 12.8618 4.86199L11.1379 3.13813C10.8776 2.87778 10.4554 2.87778 10.1951 3.13813L2.6665 10.6667V13.3334Z" stroke="#858D99" stroke-linecap="round" stroke-linejoin="round"/>
              <path d="M8 5.3335L10.6667 8.00016" stroke="#858D99" stroke-linecap="round" stroke-linejoin="round"/>
            </svg> -->
            <span>Edit</span>
          </div>
        </div>
      </div>
    </div>
    
    <CreateContract ref="createContract" />
    <ShareModal ref="shareModal" :contract="contractData" />
    <DecodeModal ref="decodeModal" :contract="contractData" />
    <GetContractModal ref="getContractModal" @confirm="getContractFun" />
    <TeamModal ref="teamModal" />
    <SourceCodeModal ref="sourceCodeModal" />
    <n-modal
      v-model:show="showHint"
      :mask-closable="false"
      class="modal-style"
      preset="card"
      :style="{width: '500px', 'border-radius': '10px', 'min-height': '200px'}"
      title="提示"
    >
      <div>
        是否确认同步,如果同步则本地修改的内容都会被覆盖
      </div>
      <div class="ft flex-center">
        <div class="cancel btn" @click="() => showHint = false">cancel</div>
        <n-spin :show="syncing" style="color: #FFF">
          <div class="ok btn" @click="sync">
            <span>{{syncing ? 'Syncing' : 'Ok'}}</span>
          </div>
        </n-spin>
      </div>
    </n-modal>
  </div>
</template>
<script>
import { ref, watch, computed, toRaw } from 'vue'
import { useUtils } from '../hooks/useUtils'
import CreateContract from '@/components/CreateContract.vue'
import ShareModal from '@/components/ShareModal.vue'
import GetContractModal from '@/components/GetContractModal.vue'
import DecodeModal from '@/components/DecodeModal.vue'
import TeamModal from '@/components/TeamModal.vue'
import SourceCodeModal from '@/components/SourceCodeModal.vue'
import Avatar from "@/components/Avatar.vue"
import { useStore } from 'vuex'
import { ethers } from 'ethers'
import { getLs, setLs } from "@/service/service";
import { useDialog, useMessage } from "naive-ui"
import { updateContract, checkContractInfo, getContract } from '../http/abi'
import { chains } from '../libs/chains'
import { formatAddress } from '../libs/utils'
export default {
  props: ['contract'],
  components: {
    CreateContract,
    ShareModal,
    GetContractModal,
    DecodeModal,
    Avatar,
    TeamModal,
    SourceCodeModal
  },
  setup(props) {
    const store = useStore()
    const dialog = useDialog()
    const message = useMessage()
    const createContract = ref(null)
    const sourceCode = ref([])
    const shareModal = ref(null)
    const decodeModal = ref(null)
    const showHint = ref(false)
    const showLoading = ref(false)
    const getContractModal = ref(null)
    const sourceCodeModal = ref(null)
    const teamModal= ref(null)
    const syncing = ref(false)
    const activeName = ref('')
    const activeIndex = ref(-1)
    const contractData = ref({})
    const balance = ref(0)

    const { toEtherscanAddress, copy, setData } = useUtils()
    
    const provider = computed(() => {
      return store.state.provider
    })
    const address = computed(() => {
      return store.state.address
    })
    const getAddress = computed(() => {
      return (value) => {
        return formatAddress(value)
      }
    })
    const isIframe = computed(() => {
      return store.state.isIframe
    })

    const showTeamModal = () => {
      teamModal.value.show(props.contract || {})
    }

    const getSourceCode = async () => {
      if (props.contract.sources && props.contract.sources.length) {
        sourceCodeModal.value.show(props.contract)
      } else {
        // 弹窗提示
        message.info('The current contract is not open source')
      }
    }

    const getContractFun = () => {
      let password = props.contract.password
      let token = props.contract.token
      syncing.value = true
      getContract({token, password}).then(res => {
        if (res.code == 1) {
          message.error(res.msg)
        } else {
          let contract = res.contract.contract_info
          let chainInfo = contract.chain_info
          let chainId = chainInfo.chainId
          let chain = chains.filter(e => e.chainId == chainId)[0]
          let sol = {
            id: props.contract.id,
            isImport: true,
            authorAddress: res.contract.authorAddress,
            name: contract.name,
            address: contract.contract_address,
            abi: JSON.parse(contract.contract_abi),
            chain: chain,
            remark: contract.description,
            token: res.contract.token,
            versionNumber: res.contract.version_number || 1,
            password
          }
          setData(sol)
          getContractModal.value.showModal = false
          message.success('Sync successfully')
        }
        syncing.value = false
        showHint.value = false
      }).catch(err => {
        console.log(err)
        message.error(err)
        syncing.value = false
        showHint.value = false
      })
    }
    const sync = async () => {
      syncing.value = true
      checkContractInfo({token: props.contract.token}).then(res => {
        console.log(res, props.contract)
        if (res.version_number == props.contract.versionNumber) {
          message.info('is latest version')
          showHint.value = false
          syncing.value = false
        } else {
          console.log(props.contract)
          if (res.openSourceType == 'Limited' && !props.contract.password) {
            getContractModal.value.showModal = true
          } else {
            getContractFun()
          }
        }
      })
    }
    const updateShare = async () => {
      let contract = props.contract
      if (contract.authorAddress && contract.authorAddress.toLocaleLowerCase() != address.value.toLocaleLowerCase()) {
        dialog.warning({
          title: "Notice",
          content: `To update this contract, Please switch the wallet address to "${contract.authorAddress}"`,
          positiveText: "Ok",
          maskClosable: false,
        })
        return
      }
      
      updateContract({
        token: contract.token,
        contract_info: {
          contract_address: contract.address,
          contract_abi: JSON.stringify(contract.abi),
          name: contract.name,
          chain_info: {
            chainName: contract.chain.chainName || contract.chain.name,
            chainId: contract.chain.chainId,
          },
          description: contract.remark
        }
      }).then(res => {
        if (res.code == 0) {
          message.success('Update successfully')
          contractData.value.hasUpdate = false
          checkContractInfo({token: contractData.value.token}).then(res => {
            contractData.value.versionNumber = res.version_number
            console.log(contractData.value)
            setData(contractData.value)
          })
        } else {
          message.error(res.msg)
        }
      }).catch (error => {
        message.error(error)
      })
    }
    const edit = () => {
      let { abi, address, chain, createAt, id, name, token, authorAddress, versionNumber = 1, userList = [] } = props.contract
      let chainId = ''
      if (chain && chain.chainId) chainId = chain.chainId
      abi = JSON.stringify(abi)
      let formData = {abi, address, chainId, createAt, id, name, token, authorAddress, versionNumber, userList}
      createContract.value.show()
      createContract.value.formData = formData
    }
    const share = () => {
      shareModal.value.showModal = true
    }
    const decode = () => {
      decodeModal.value.showModal = true
    }
    const update = (name, index) => {
      let el = document.querySelector('.source-tabs-w')
      let el1 = el.querySelectorAll('.source-tab-item')[index]
      let scrollLeft = el1.offsetLeft
      const containWidth = el.offsetWidth
      console.log(scrollLeft, containWidth)
      let resultSpot = scrollLeft - 160 - containWidth / 2 
      activeName.value = name
      activeIndex.value = index
      el.scrollTo((resultSpot + 50), 100)
    }
    const domMove = (i) => {
      let el = document.querySelector('.source-tabs-w')
      let scrollLeft = el.scrollLeft
      if (i == 1) {
        if (scrollLeft > 140) {
          el.scrollLeft = scrollLeft - 140
        } else {
          el.scrollLeft = 0
        }
      } else if (i == 2) {
        el.scrollLeft = scrollLeft + 140
      }
    }
    const del = () => {
      dialog.warning({
        title: "Notice",
        content: "This operation will permanently delete the contract information, do you want to continue？",
        positiveText: "Ok",
        negativeText: "Cancel",
        maskClosable: false,
        onPositiveClick: async () => {
          let menuList = await getLs('menuList') || []
          let contractList = await getLs('contractList') || []
          let results = await getLs('results') || {}
          let id = props.contract.id
          for (let i = 0; i < menuList.length; i++) {
            let son = menuList[i].son
            son.forEach((e, index) => {
              if (e.id == id) {
                son.splice(index, 1)
              }
            })
            menuList[i].son = son
          }
          contractList.forEach((e, index) => {
            if (e.id == id) {
              contractList.splice(index, 1)
            }
          })
          if (results[id]) {
            delete results[id]
          }
          setLs('activeId', '').then(() => {
            store.commit('setActiveId', '')
          })
          setLs('contractList', JSON.parse(JSON.stringify(contractList))).then(res => {
            console.log(res)
            store.commit("setContractList", res)
          })
          setLs('menuList', JSON.parse(JSON.stringify(menuList))).then(res => {
            console.log(res)
            store.commit("setMenuList", res)
          })
          setLs('results', JSON.parse(JSON.stringify(results))).then(res => {
            console.log(res)
            store.commit("setResults", res)
          })
        }
      })
    }
    watch(() => props.contract, async (val) => {
      if (val && provider.value) {
        let balanceEth = await toRaw(provider.value).getBalance(val.address)
        let balanceInEth = await ethers.utils.formatEther(balanceEth)
        balance.value = balanceInEth
      } else {
        balance.value = 0
      }
      contractData.value = props.contract
      if (props.contract.isImport && props.contract.token) {
        checkContractInfo({token: props.contract.token}).then(res => {
          if (!contractData.value.authorAddress) {
            contractData.value.authorAddress = res.authorAddress
            setData(toRaw(contractData.value))
          }
          let versionNumber = props.contract.versionNumber || 1
          let resVersionNumber = res.version_number || 1
          if (resVersionNumber == versionNumber) {
            contractData.value.hasSync = false
          } else {
            contractData.value.hasSync = true
          }
        })
      }
    }, {immediate: true})
    return {
      sourceCodeModal,
      isIframe,
      teamModal,
      balance,
      decodeModal,
      syncing,
      showHint,
      address,
      getContractModal,
      showLoading,
      activeIndex,
      activeName,
      sourceCode,
      contractData,
      createContract,
      del,
      shareModal,
      edit,
      copy,
      share,
      toEtherscanAddress,
      getSourceCode,
      update,
      domMove,
      updateShare,
      sync,
      getContractFun,
      decode,
      getAddress,
      showTeamModal
    }
  }
}
</script>
<style lang="scss" scoped>
.hd {
  .hd-section {
    .title {
      font-family: Montserrat-Bold;
      font-size: 30px;
      line-height: 40px;
      color: #FFFFFF;
      flex: 1;
      overflow: hidden;
      white-space: nowrap;
      text-overflow: ellipsis;
    }
    .title-btn-item {
      margin-left: 8px;
      font-weight: 400;
      font-size: 12px;
      line-height: 16px;
      color: #FFFFFF;
      padding: 0 10px;
      height: 26px;
      box-sizing: border-box;
      background: #2C2D34;
      border-radius: 6px;
      &:hover {
        background: #302E38 !important;
      }
      img {
        width: 20px;
        height: 20px;
        margin-right: 8px;
      }
    }
    .hd-btns {
      // width: 754px;
      // flex: 0 0 754px;
      // margin-left: 20px;
      justify-content: flex-end;
      .hd-btn-item {
        font-weight: 400;
        font-size: 12px;
        line-height: 16px;
        color: #FFFFFF;
        padding: 0 12px;
        box-sizing: border-box;
        height: 40px;
        background: #2C2D34;
        border-radius: 10px;
        cursor: pointer;
        margin-left: 12px;
        &:hover {
          background: #3D3D48;
          svg {
            path {
              stroke: #FFFFFF;
            }
          }
        }
        img {
          width: 16px;
          height: 16px;
        }
        svg {
          flex: 0 0 16px;
          width: 16px;
          height: 16px;
        }
        span {
          margin-left: 8px;
        }
        &.hd-btn-item-red {
          background: #F43658 !important;
          &:hover {
            background: #EF5671 !important;
          }
        }
        &.hover-0670A6 {
          background: #0784C3;
          &:hover {
            background: #0670A6 !important;
          }
        }
        &.hover-6F4AC5 {
          &:hover {
            background: #6F4AC5 !important;
          }
        }
        &.hover-F43658 {
          &:hover {
            background: #F43658 !important;
          }
        }
        &.hover-57B36F {
          &:hover {
            background: #57B36F !important;
          }
        }
        &.hd-btn-item-h {
          justify-content: flex-start;
          transition: all .5s;
          max-width: 40px;
          overflow: hidden;
          span {
            transition: all .5s;
            opacity: 0;
            white-space: nowrap;
          }
          &:hover {
            max-width: 150px;
            span {
              opacity: 1;
            }
          }
        }
      }
    }
  }
  .desc {
    font-weight: 400;
    font-size: 12px;
    line-height: 16px;
    text-transform: capitalize;
    color: #858D99;
    margin-top: 16px;
  }
  .info {
    margin-top: 18px;
    .info-line {
      height: 20px;
      width: 1px;
      background: rgba(133, 141, 153, 0.15);
      margin: 0 24px;
    }
    .info-item {
      .info-key {
        font-family: 'Montserrat';
        font-style: normal;
        font-weight: 400;
        font-size: 13px;
        line-height: 16px;
        text-transform: capitalize;
        color: #858D99;
      }
      .info-value {
        font-family: 'Montserrat-Medium';
        font-style: normal;
        font-size: 13px;
        line-height: 16px;
        text-transform: capitalize;
        color: #FFFFFF;
        margin-left: 10px;
        &.info-value-a {
          cursor: pointer;
          &:hover {
            color: #0784C3;
          }
        }
      }
      svg {
        width: 16px;
        height: 16px;
        margin-left: 6px;
        cursor: pointer;
        &:hover {
          path {
            stroke: #FFFFFF
          }
        }
      }
    }
    .team {
      font-weight: 400;
      font-size: 13px;
      line-height: 16px;
      text-transform: capitalize;
      color: #858D99;
      .user-list {
        margin-left: 18px;
        .user-avatar {
          border: 1.5px solid #FFFFFF;
          cursor: pointer;
          width: 32px;
          height: 32px;
          border-radius: 50%;
          margin-left: -8px;
          position: relative;
          box-sizing: border-box;
          .more {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            background: #2C2D34;
            font-family: 'Montserrat-Medium';
            font-size: 12px;
            line-height: 12px;
            color: #FFFFFF;
            position: relative;
            &:hover {
              .more-list {
                display: block;
              }
            }
            .more-list {
              display: none;
              position: absolute;
              right: 0;
              top: 44px;
              width: 160px;
              max-height: 200px;
              overflow-y: auto;
              background: #2C2D34;
              border: 1px solid rgba(133, 141, 153, 0.1);
              box-shadow: 0px 12px 30px rgba(10, 10, 12, 0.3);
              backdrop-filter: blur(10px);
              border-radius: 6px;
              padding: 10px 12px;
              .user-item {
                width: 100%;
                height: 30px;
                .item-avatar {
                  width: 18px;
                  height: 18px;
                  border-radius: 50%;
                }
                span {
                  font-size: 13px;
                  line-height: 16px;
                  text-transform: capitalize;
                  color: #FFFFFF;
                  flex: 1;
                  overflow: hidden;
                  text-overflow: ellipsis;
                  white-space: nowrap;
                  margin-left: 6px;
                }
              }
            }
          }
        }
      }
      .team-edit {
        margin-left: 12px;
        cursor: pointer;
        &:hover {
          span {
            color: #FFFFFF;
          }
        }
      }
    }
  }
}
.source-tabs-b {
  position: relative;
  background: #2C2D34;
  height: 34px;
  padding-right: 60px;
  box-sizing: border-box;
}
.source-tabs-right {
  position: absolute;
  background: #2C2D34;
  width: 60px;
  position: absolute;
  height: 40px;
  right: 0;
  top: 0;
  z-index: 9;
  padding: 0 8px;
  box-sizing: border-box;
  svg {
    cursor: pointer;
  }
  &::before {
    content: '';
    width: 1px;
    height: 12px;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    margin: auto;
    z-index: 2;
    background: rgba(133, 141, 153, 0.2);
  }
}
.source-tabs-w {
  max-width: 100%;
  overflow-x: auto;
  scrollbar-width: none;
  border-radius: 10px 10px 0 0;
  box-sizing: border-box;
  background: #2C2D34;
  &::-webkit-scrollbar {
    display: none;
  }
  .source-tbas {
    height: 40px;
    .source-tab-item {
      flex: 0 0 140px;
      cursor: pointer;
      position: relative;
      svg {
        display: none;
      }
      .source-tab-item-content {
        position: relative;
        background: #2C2D34;
        z-index: 1;
        width: 140px;
        height: 40px;
        padding: 0 12px;
        box-sizing: border-box;
        font-family: 'Montserrat-Medium';
        font-size: 12px;
        line-height: 16px;
        color: #858D99;
        span {
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
        }
      }
      &::before {
        content: '';
        width: 1px;
        height: 12px;
        position: absolute;
        top: 0;
        bottom: 0;
        right: 0;
        margin: auto;
        z-index: 2;
        background: rgba(133, 141, 153, 0.2);
      }
      &::after {
        content: '';
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        z-index: 0;
        background: linear-gradient( to bottom, #2C2D34 40%, #17171A 60%);
      }
      &:hover {
        .source-tab-item-content {
          background: #2A2A32;
          border-radius: 10px 10px 0px 0px;
          color: #FFFFFF;
          svg {
            display: inline-block;
          }
        }
      }
      &:first-child {
        border-top-left-radius: 10px;
        overflow: hidden;
      }
      &:last-child {
        border-top-right-radius: 10px;
        overflow: hidden;
        &::before {
          display: none;
        }
      }
      &.source-tab-item-activated {
        &::before {
          display: none;
        }
        .source-tab-item-content {
          color: #FFFFFF;
          background: #17171A;
          border-radius: 10px 10px 0px 0px;
          svg {
            display: inline-block;
          }
        }
        & + .source-tab-item {
          .source-tab-item-content {
            border-radius: 0px 0px 0px 10px;
          }
        }
      }
      &.source-tab-item-activated-prev {
        &::before {
          display: none;
        }
        .source-tab-item-content {
          border-radius: 0px 0px 10px 0px;
        }
      }
    }
  }
}
.source-pane {
  height: calc(80vh - 40px);
  overflow: auto;
  border-radius: 0 0 10px 10px;
}
.ft {
  justify-content: flex-end;
  margin-top: 20px;
  .ok {
    margin-left: 20px;
    background: #375CFF;
  }
  .cancel {
    background: rgba(133, 141, 153, 0.1);
  }
  .btn {
    padding: 5px 16px;
    box-sizing: border-box;
    border-radius: 5px;
    cursor: pointer;
  }
}
</style>
<style>
  .hljs {
    background: #17171A !important;
  }
  .custom-card .n-spin-content {
    border: 1px solid rgba(133, 141, 153, 0.1);
    border-radius: 10px;
  }
</style>
