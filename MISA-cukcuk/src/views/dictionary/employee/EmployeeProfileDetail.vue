<template>
  <div>
    <!-- <button id="btnAdd" class="m-btn m-btn-default" v-on:click="btnAddOnClick">
      <div class="m-btn-icon icon-add"></div>
      <div class="btn-text">Thêm nhân viên</div>
    </button> -->
    <div
      class="m-dialog dialog-detail"
      title="Thông tin nhân viên"
      :class="{ isHide: isHide }"
    >
      <div class="dialog-modal"></div>
      <div class="dialog-content">
        <div class="dialog-header" @mousedown="handleDrag">
          <div class="dialog-header-title">THÔNG TIN NHÂN VIÊN</div>
          <div class="dialog-header-close">
            <button v-on:click="btnCancelOnClick">x</button>
          </div>
        </div>
        <div class="dialog-body">
          <div class="m-row m-flex">
            <div class="m-col el-avatar-employee m-flex-1">
              <div class="el-avatar"></div>
              <div class="el-avatar-note text-align-center">
                (Vui lòng chọn ảnh có định dạng <br /><b
                  >.jpg, .jpeg, .png, .gif. </b
                >)
              </div>
            </div>
            <div class="m-col el-left m-flex-4">
              <div class="group-label-info">A. Thông tin chung:</div>
              <hr class="hr-group-label" />
              <div class="m-row mg-top-0 m-flex">
                <div class="m-col m-flex-1">
                  <div class="m-label">
                    Mã nhân viên (<span class="label-required">*</span>)
                  </div>
                  <div class="m-control">
                    <input
                      id="txtEmployeeCode"
                      fieldName="EmployeeCode"
                      required
                      class="input-required"
                      type="text"
                      v-model="employee.EmployeeCode"
                    />
                  </div>
                </div>
                <div class="m-flex-1 mg-left-10px">
                  <div class="m-label">
                    Họ và tên (<span class="label-required">*</span>)
                  </div>
                  <div class="m-control">
                    <input
                      id="txtFullName"
                      fieldName="FullName"
                      class="input-required"
                      type="text"
                      required
                      v-model="employee.FullName"
                    />
                  </div>
                </div>
              </div>
              <div class="m-row m-flex">
                <div class="m-flex-1">
                  <div class="m-label">Ngày sinh</div>
                  <input
                    class="m-combobox-input"
                    type="date"
                    autocomplete="off"
                  />
                </div>
                <div class="m-flex-1 mg-left-10px">
                  <div class="m-label">Giới tính</div>
                  <select id="cbxGender" class="m-control">
                    <option value="1">Nam</option>
                    <option value="0">Nữ</option>
                  </select>
                </div>
              </div>
              <div class="m-row m-flex">
                <div class="m-flex-1">
                  <div
                    class="m-label"
                    title="Số chứng minh thư nhân dân hoặc căn cước công dân"
                  >
                    Số CMTND/ Căn cước (<span class="label-required">*</span>)
                  </div>
                  <div class="m-control">
                    <input
                      id="txtIdentityNumber"
                      fieldName="text"
                      type="text"
                      required
                      v-model="employee.IdentityNumber"
                    />
                  </div>
                </div>
                <div class="m-flex-1 mg-left-10px">
                  <div class="m-label">Ngày cấp</div>
                  <input
                    class="m-combobox-input"
                    type="date"
                    autocomplete="off"
                    v-model="employee.IdentityDate"
                  />
                </div>
              </div>
              <div class="m-row m-flex">
                <div class="m-flex-1">
                  <div class="m-label">Nơi cấp</div>
                  <div class="m-control">
                    <input
                      id="txtIdentityPlace"
                      fieldName="PhoneNumber"
                      class="input-required"
                      type="text"
                    />
                  </div>
                </div>
                <div class="m-flex-1"></div>
              </div>
              <div class="m-row m-flex">
                <div class="m-col m-flex-1">
                  <div class="m-label">
                    Email (<span class="label-required">*</span>)
                  </div>
                  <div class="m-control">
                    <input
                      id="txtEmail"
                      fieldName="Email"
                      type="email"
                      required
                      placeholder="example@domain.com"
                      v-model="employee.Email"
                    />
                  </div>
                </div>
                <div class="m-flex-1 mg-left-10px">
                  <div class="m-label">
                    Số điện thoại (<span class="label-required">*</span>)
                  </div>
                  <div class="m-control">
                    <input
                      id="txtPhoneNumber"
                      fieldName="FullName"
                      class="input-required"
                      type="text"
                      required
                      v-model="employee.PhoneNumber"
                    />
                  </div>
                </div>
              </div>
              <div class="group-label-info" style="margin-top: 30px">
                B. Thông tin công việc:
              </div>
              <hr class="hr-group-label" />
              <div class="m-row m-flex">
                <div class="m-flex-1">
                  <div class="m-label">Vị trí</div>
                  <select
                    id="cbxPosition"
                    fieldName="CustomerGroupName"
                    fieldValue="CustomerGroupId"
                    api="/api/customergroups"
                    class="m-control"
                  >
                    <option value="19165ed7-212e-21c4-0428-030d4265475f">
                      Giám đốc
                    </option>
                    <option value="19165ed7-212e-21c4-0428-030d4265475f">
                      Nhân viên
                    </option>
                  </select>
                </div>
                <div class="m-flex-1 mg-left-10px">
                  <div class="m-label">Phòng ban</div>
                  <select
                    id="cbnDepartment"
                    fieldName="CustomerGroupName"
                    fieldValue="CustomerGroupId"
                    api="/api/customergroups"
                    class="m-control"
                  >
                    <option value="19165ed7-212e-21c4-0428-030d4265475f">
                      Phòng nhân sự
                    </option>
                    <option value="19165ed7-212e-21c4-0428-030d4265475f">
                      Phòng đào tạo
                    </option>
                  </select>
                </div>
              </div>
              <div class="m-row m-flex">
                <div class="m-flex-1">
                  <div class="m-label">Mã số thuế cá nhân</div>
                  <div class="m-control">
                    <input id="txtAddress" fieldName="Address" type="text" />
                  </div>
                </div>
                <div class="m-flex-1 mg-left-10px">
                  <div class="m-label">Mức lương cơ bản</div>
                  <div class="m-control">
                    <input
                      id="txtSalary"
                      fieldName="Salary"
                      type="text"
                      style="text-align: right; padding-right: 56px"
                    /><span class="currency-for-input">(VNĐ)</span>
                  </div>
                </div>
              </div>
              <div class="m-row m-flex">
                <div class="m-flex-1">
                  <div class="m-label">Ngày gia nhập</div>
                  <input
                    class="m-combobox-input"
                    type="date"
                    autocomplete="off"
                  />
                </div>
                <div class="m-flex-1 mg-left-10px">
                  <div class="m-label">Tình trạng công việc</div>
                  <select
                    id="cboWorkStatus"
                    fieldName="CustomerGroupName"
                    fieldValue="CustomerGroupId"
                    api="/api/customergroups"
                    class="m-control"
                  >
                    <option value="19165ed7-212e-21c4-0428-030d4265475f">
                      Đang làm việc
                    </option>
                    <option value="19165ed7-212e-21c4-0428-030d4265475f">
                      Đang thử việc
                    </option>
                    <option value="19165ed7-212e-21c4-0428-030d4265475f">
                      Nghỉ việc
                    </option>
                  </select>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="dialog-footer">
          <button
            id="btnCancel"
            class="m-btn m-btn-default m-btn-cancel"
            v-on:click="btnCancelOnClick"
          >
            Hủy
          </button>
          <button
            id="btnSave"
            class="m-btn m-btn-default"
            @click="saveEmployee"
          >
            <i class="far fa-save"></i><span class="btn-text">Lưu</span>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
// import axios from "axios";

export default {
  components: {},

  methods: {
    handleDrag(e) {
      let pos1 = 0,
        pos2 = 0,
        pos3 = 0,
        pos4 = 0;

      let dialog = document.querySelector(".dialog-content");
      dragMouseDown(e);

      function dragMouseDown(e) {
        e = e || window.event;
        e.preventDefault();
        // get the mouse cursor position at startup:
        pos3 = e.clientX;
        pos4 = e.clientY;
        document.onmouseup = closeDragElement;
        // call a function whenever the cursor moves:
        document.onmousemove = elementDrag;
      }

      function elementDrag(e) {
        e = e || window.event;
        e.preventDefault();
        // calculate the new cursor position:
        pos1 = pos3 - e.clientX;
        pos2 = pos4 - e.clientY;
        pos3 = e.clientX;
        pos4 = e.clientY;
        // set the element's new position:
        dialog.style.top = dialog.offsetTop - pos2 + "px";
        dialog.style.left = dialog.offsetLeft - pos1 + "px";
      }

      function closeDragElement() {
        // stop moving when mouse button is released:
        document.onmouseup = null;
        document.onmousemove = null;
      }
    },

    btnAddOnClick() {},

    btnCancelOnClick() {
      this.$emit("closePopup", true);
    },

    rowOnClick(employee) {
      alert(employee.FullName);
    },

    async saveEmployee() {
      // const response = await axios.post(
      //     "http://api.manhnv.net/api/employees"
      // );
      console.log("Save employee");
    },
  },

  data() {
    return {
      dialog: false,
      display: "none",
      employee: {
        EmployeeId: "12693b29-274c-35ce-d11d-086412a8ea97",
        EmployeeCode: "NV-247247",
        FirstName: "Trương Phương",
        LastName: "Minh",
        FullName: "Mai Thị Bích",
        Gender: null,
        DateOfBirth: "1992-06-17T00:00:00",
        PhoneNumber: "0995194058",
        Email: "kute@example.com",
        Address: "319 Prospect Hill Blvd, Keith Bldg, Boise, Idaho, 76994",
        IdentityNumber: "25323252050",
        IdentityDate: null,
        IdentityPlace: "Hà Nội",
        JoinDate: "2014-12-05T00:00:00",
        MaritalStatus: 5,
        PersonalTaxCode: "06951619",
        Salary: 16275117,
        EducationalBackground: 5,
        WorkStatus: 2,
        PositionId: "25c6c36e-1668-7d10-6e09-bf1378b8dc91",
        PositionName: "Thu ngân",
        DepartmentId: "142cb08f-7c31-21fa-8e90-67245e8b283e",
        DepartmentName: "Phòng Marketting",
        QualificationId: "3541ff76-58f0-6d1a-e836-63d5d5eff719",
        QualificationName: "Kỹ sư CNTT",
        GenderName: "Không xác định",
        WorkStatusName: "Đang thử việc",
      },
    };
  },

  props: {
    isHide: Boolean,
  },
};
</script>

<style scoped>
.isHide {
  display: none;
  visibility: hidden;
}
.m-dialog {
  z-index: 999;
}

.dialog-header {
  position: sticky;
  top: 0%;
  height: 40px;
  line-height: 60px;
  padding-left: 16px;
  padding-bottom: 10px;
  display: flex;
  font-size: 24px;
  background-color: #fff;
}

.dialog-header:hover {
  cursor: move;
}

.dialog-header-close {
  position: absolute;
  right: 16px;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  cursor: pointer;
  top: 10px;
  align-items: center;
  border: none;
  background-color: transparent;
  font-size: 24px;
  line-height: 24px;
}
.dialog-modal {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: black;
  opacity: 0.4;
  z-index: inherit;
}

.dialog-content {
  position: fixed;
  border-radius: 5px;
  width: 750px;
  height: 500px;
  background-color: #fff;
  left: calc(50% - 375px);
  top: calc(50% - 250px);
  overflow: auto;
  z-index: inherit;
}
.dialog-body {
  padding: 0 16px 16px 16px;
}
.dialog-footer {
  position: sticky;
  bottom: 0%;
  display: flex;
  width: 100%;
  height: 60px;
  background-color: #e9ebee;
  border-radius: 0 0 5px 5px;
  align-items: center;
  justify-content: flex-end;
  padding: 12px 24px;
  box-sizing: border-box;
}
.el-avatar-employee {
  padding-top: 16px;
  padding-right: 16px;
}
.el-avatar-note {
  font-size: 12px;
}
.el-avatar-employee .el-avatar {
  border: 1px solid #ccc;
  width: 160px;
  height: 160px;
  margin: 0 auto;
  border-radius: 50%;
  cursor: pointer;
  background-image: url(/content/img/default-avatar.jpg);
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
.currency-for-input {
  position: absolute;
  right: 40px;
  line-height: 40px;
  font-style: italic;
}
</style>