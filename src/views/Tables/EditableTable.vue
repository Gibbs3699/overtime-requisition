<template>
    <b-row>
      <b-col md="12">
        <iq-card>
          <template v-slot:headerTitle>
            <h4 class="card-title">name.... Over Time Requisition</h4>
          </template>
          <template v-slot:body>
            <b-row>
              <b-col md="12" class="table-responsive">
                <b-table bordered hover :items="rows" :fields="columns" foot-clone>
                  <template v-slot:cell(date)="data">
                    <span v-if="!data.item.editable">{{ data.item.date }}</span>
                    <input type="text" v-model="data.item.date" v-else class="form-control">
                  </template>
                  <template v-slot:cell(time)="data">
                    <span v-if="!data.item.editable">{{ data.item.time }}</span>
                    <input type="text" v-model="data.item.time" v-else class="form-control">
                  </template>
                  <template v-slot:cell(remark)="data">
                    <span v-if="!data.item.editable">{{ data.item.remark }}</span>
                    <input type="text" v-model="data.item.remark" v-else class="form-control">
                  </template>
                  <template v-slot:cell(status)="data">
                    <span v-if="!data.item.editable">{{ data.item.status }}</span>
                    <input type="text" v-model="data.item.status" v-else class="form-control">
                  </template>
                  <template v-slot:cell(approved)="data">
                    <span v-if="!data.item.editable">{{ data.item.approved}}</span>
                    <input type="text" v-model="data.item.approved" v-else class="form-control">
                  </template>
                </b-table>
              </b-col>
            </b-row>
          </template>
        </iq-card>
                <iq-card>
          <template v-slot:headerTitle>
            <h4 class="card-title">DEDE Over Time Requisition list on .... </h4>
          </template>
          <template v-slot:body>
            <b-row>
              <b-col md="12" class="table-responsive">
                <b-table bordered hover :items="rows" :fields="columns" foot-clone>
                  <template v-slot:cell(date)="data">
                    <span v-if="!data.item.editable">{{ data.item.date }}</span>
                    <input type="text" v-model="data.item.date" v-else class="form-control">
                  </template>
                  <template v-slot:cell(time)="data">
                    <span v-if="!data.item.editable">{{ data.item.time }}</span>
                    <input type="text" v-model="data.item.time" v-else class="form-control">
                  </template>
                  <template v-slot:cell(remark)="data">
                    <span v-if="!data.item.editable">{{ data.item.remark }}</span>
                    <input type="text" v-model="data.item.remark" v-else class="form-control">
                  </template>
                  <template v-slot:cell(status)="data">
                    <span v-if="!data.item.editable">{{ data.item.status }}</span>
                    <input type="text" v-model="data.item.status" v-else class="form-control">
                  </template>
                  <template v-slot:cell(approved)="data">
                    <span v-if="!data.item.editable">{{ data.item.approved}}</span>
                    <input type="text" v-model="data.item.approved" v-else class="form-control">
                  </template>
                </b-table>
              </b-col>
            </b-row>
          </template>
        </iq-card>
      </b-col>
    </b-row>
</template>
<script>
import { socialvue } from '../../config/pluginInit'

export default {
  name: 'EditableTable',
  mounted () {
    socialvue.index()
  },
  methods: {
    add () {
      let obj = this.default()
      this.rows.push(obj)
    },
    default () {
      return {
        id: this.rows.length,
        employeeNumber: '',
        devision: '',
        department: '',
        subGroup: '',
        status: '2011/04/25',
        phone: '$0'
      }
    },
    submit (item) {
      item.editable = false
    },
    remove (item) {
      let index = this.rows.indexOf(item)
      this.rows.splice(index, 1)
    }
  },
  data () {
    return {
      columns: [
        { label: 'Date', key: 'date', class: 'text-left' },
        { label: 'Time', key: 'time', class: 'text-left' },
        { label: 'Remarks', key: 'remark', class: 'text-left' },
        { label: 'Status', key: 'status', class: 'text-left' },
        { label: 'Approved By', key: 'approved', class: 'text-left' }
      ],
      rows: [
        {
          id: 1,
          name: 'Tiger Nixon',
          position: 'System Architect',
          office: 'Edinburgh',
          age: '61',
          date: '2011/04/25',
          salary: '$320,800'
        },
        {
          id: 2,
          name: 'Garrett Winters',
          position: 'Accountant',
          office: 'Tokyo',
          age: '63',
          date: '2011/06/19',
          salary: '$200,600'
        },
        {
          id: 3,
          name: 'Ashton Cox',
          position: 'Junior Technical Author',
          office: 'San Francisco',
          age: '69',
          date: '2011/01/20',
          salary: '$140,500'
        }
      ]
    }
  }
}
</script>
