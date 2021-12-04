<template>
    <b-row>
     <b-col>
        <iq-card class="table-padding-top">
          <template v-slot:headerTitle>
            <h4 class="card-title">Today's Request</h4>
          </template>
          <template v-slot:body>
            <b-row>
              <b-col md="12" class="table-responsive">
                <b-table bordered hover :items="rows" :fields="columns">
                  <template v-slot:cell(name)="data">
                    <span v-if="!data.item.editable">{{ data.item.name }}</span>
                    <input type="text" v-model="data.item.name" v-else class="form-control">
                  </template>
                  <template v-slot:cell(employeeNumber)="data">
                    <span v-if="!data.item.editable">{{ data.item.employeeNumber }}</span>
                    <input type="text" v-model="data.item.employeeNumber" v-else class="form-control">
                  </template>
                  <template v-slot:cell(devisionDepartment)="data">
                    <span v-if="!data.item.editable">{{ data.item.devisionDepartment }}</span>
                    <input type="text" v-model="data.item.devisionDepartment" v-else class="form-control">
                  </template>
                  <template v-slot:cell(subGroup)="data">
                    <span v-if="!data.item.editable">{{ data.item.subGroup }}</span>
                    <input type="text" v-model="data.item.subGroup" v-else class="form-control">
                  </template>
                  <template v-slot:cell(overtime)="data">
                    <span v-if="!data.item.editable">{{ data.item.overtime }}</span>
                    <input type="text" v-model="data.item.overtime" v-else class="form-control">
                  </template>
                  <template v-slot:cell(approvedBy)="data">
                    <span v-if="!data.item.editable">{{ data.item.approvedBy }}</span>
                    <input type="text" v-model="data.item.approvedBy" v-else class="form-control">
                  </template>
                  <template v-slot:cell(approvedStatus)="data">
                    <span v-if="!data.item.editable">{{ data.item.approvedStatus }}</span>
                    <input type="text" v-model="data.item.approvedStatus" v-else class="form-control">
                  </template>
                </b-table>
              </b-col>
            </b-row>
          </template>
        </iq-card>
      </b-col>
      <b-col cols="12" >
        <div class="iq-card mb-0" style="border-bottom-left-radius: 0; border-bottom-right-radius: 0" id="menu">
          <div id="menu-navi" class="iq-card-body d-flex align-items-center justify-content-between" @click="onClickNavi($event)">
            <button type="button" class="btn mr-1 btn-outline-primary" data-action="move-today">Today</button>
            <div class="d-flex">
              <button type="button" class="btn btn-link iq-bg-primary" data-action="move-prev">
                <i class="fa fa-chevron-left mr-0" data-action="move-prev" />
              </button>
              <h5 id="renderRange" class="render-range mt-1 mx-4">{{ dateRange }}</h5>
              <button type="button" class="btn btn-link iq-bg-primary" data-action="move-next">
                <i class="fa fa-chevron-right mr-0" data-action="move-prev" />
              </button>
            </div>
            <div>
              <b-form-radio-group
                id="btn-radios-1"
                v-model="selectedView"
                :options="viewModeOptions"
                buttons
                button-variant="primary"
                name="radios-btn-default"
              ></b-form-radio-group>
            </div>
          </div>
        </div>
      </b-col>
      <b-col cols="12">
        <calendar style="height: 800px" id="calender"
                  ref="tuiCal"
                  :useDetailPopup="useDetailPopup"
                  :view="selectedView"
                  :calendars="calendarList"
                  :schedules="scheduleList"
                  :template="template"
                  :taskView="true"
                  :scheduleView="true"
                  :month="month"
                  :disableDblClick="disableDblClick"
                  :isReadOnly="isReadOnly"
                  @clickSchedule="onClickSchedule"
                  @clickDayname="onClickDayname"
                  @beforeCreateSchedule="onBeforeCreateSchedule"
                  @beforeUpdateSchedule="onBeforeUpdateSchedule"
                  @beforeDeleteSchedule="onBeforeDeleteSchedule"
        />
      </b-col>
    </b-row>
</template>
<script>
import 'tui-time-picker/dist/tui-time-picker.css'
import 'tui-date-picker/dist/tui-date-picker.css'
import 'tui-calendar/dist/tui-calendar.css'
import Event from '../../../Model/Event'
import { CalenderList, Events } from '../../../FackApi/api/calendar'
import { Calendar } from '@toast-ui/vue-calendar'
import { socialvue } from '../../../config/pluginInit'
export default {
  name: 'App',
  components: {
    'calendar': Calendar
  },
  data () {
    return {
      viewModeOptions: [
        {
          text: 'Monthly',
          value: 'month'
        }
      ],
      dateRange: '',
      selectedView: 'month',
      calendarList: CalenderList,
      scheduleList: [],
      template: {
        milestone (schedule) {
          return `<span style="color:#3F3F3F;background-color: ${schedule.bgColor};">${schedule.title}</span>`
        },
        milestoneTitle () {
          return '<span class="tui-full-calendar-left-content">Milestone</span>'
        },
        allday (schedule) {
          return `<i class="fa fa-users"></i> ${schedule.title}`
        },
        alldayTitle () {
          return '<span class="tui-full-calendar-left-content">All Day</span>'
        }
      },
      month: {
        startDayOfWeek: 0
      },
      taskView: true,
      scheduleView: true,
      useDetailPopup: true,
      disableDblClick: true,
      isReadOnly: false,
      columns: [
        { label: 'Name', key: 'name', class: 'text-left' },
        { label: 'Employee Number', key: 'employeeNumber', class: 'text-left' },
        { label: 'Devision/Department', key: 'devisionDepartment', class: 'text-left' },
        { label: 'Sub Gruop', key: 'subGroup', class: 'text-left' },
        { label: 'Overtime', key: 'overtime', class: 'text-left' },
        { label: 'Approved by', key: 'approvedBy', class: 'text-left' },
        { label: 'Approved Status', key: 'approvedStatus', class: 'text-left' }
      ],
      rows: [
        {
          id: 1,
          name: 'TheGIZzzz',
          employeeNumber: 1212312121,
          devisionDepartment: 'Marvel',
          subGroup: 'Ant man',
          overtime: '20.00',
          approvedBy: 'God',
          approvedStatus: 'Yessss'
        }
      ]
    }
  },
  watch: {
    selectedView (newValue) {
      this.$refs.tuiCal.invoke('changeView', newValue, true)
      this.setRenderRangeText()
    }
  },
  methods: {
    init () {
      this.setRenderRangeText()
    },
    setRenderRangeText () {
      const { invoke } = this.$refs.tuiCal
      const view = invoke('getViewName')
      const calDate = invoke('getDate')
      const rangeStart = invoke('getDateRangeStart')
      const rangeEnd = invoke('getDateRangeEnd')
      const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
      let year = calDate.getFullYear()
      let month = calDate.getMonth() + 1
      let date = calDate.getDate()
      let dateRangeText = ''
      let endMonth, endDate, start, end
      switch (view) {
        case 'month':
          dateRangeText = `${months[month]} ${year}`
          break
        case 'week':
          year = rangeStart.getFullYear()
          month = rangeStart.getMonth() + 1
          date = rangeStart.getDate()
          endMonth = rangeEnd.getMonth() + 1
          endDate = rangeEnd.getDate()
          start = `${months[month]} ${date}`
          end = `${endDate} ${months[endMonth]}, ${year}`
          dateRangeText = `${start} - ${end}`
          break
        default:
          dateRangeText = `${date} ${months[month]} ${year}`
      }
      this.dateRange = dateRangeText
    },
    onClickNavi (event) {
      if (event.target.tagName === 'BUTTON' || event.target.tagName === 'I') {
        const { target } = event
        let action = target.dataset ? target.dataset.action : target.getAttribute('data-action')
        action = action.replace('move-', '')
        this.$refs.tuiCal.invoke(action)
        this.setRenderRangeText()
      }
    },
    onClickSchedule (res) {
      console.group('onClickSchedule')
      console.log('MouseEvent : ', res.event)
      console.log('Calendar Info : ', res.calendar)
      console.log('Schedule Info : ', res.schedule)
      console.groupEnd()
    },
    onClickDayname (res) {
      // view : week, day
      console.group('onClickDayname')
      console.log(res.date)
      console.groupEnd()
    },
    onBeforeUpdateSchedule (res) {
      const idx = this.scheduleList.findIndex(item => item.id === res.schedule.id)
      let updatedEvent = { ...res.schedule, ...res.changes }
      this.$set(this.scheduleList, idx, new Event(updatedEvent))
    },
    onBeforeCreateSchedule (res) {
      let event = new Event(res)
      this.scheduleList.push(event)
    },
    onBeforeDeleteSchedule (res) {
      const idx = this.scheduleList.findIndex(item => item.id === res.schedule.id)
      this.scheduleList.splice(idx, 1)
    },
    add () {
      let obj = this.default()
      this.rows.push(obj)
    },
    default () {
      return {
        id: this.rows.length,
        name: '',
        employeeNumber: '',
        devisionDepartment: '',
        subGroup: '',
        overtime: '',
        approvedBy: '',
        approvedStatus: ''
      }
    },
    remove (item) {
      let index = this.rows.indexOf(item)
      this.rows.splice(index, 1)
    }
  },
  mounted () {
    this.init()
    socialvue.index()
    this.scheduleList = Events
  }
}
</script>

<style lang="css" scoped>
.container-width{
  width: 100% !important;
}
.table-margin-top{
  margin-top: 3rem;
}
</style>
