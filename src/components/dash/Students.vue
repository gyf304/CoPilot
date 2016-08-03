<template>
  <section class="content">
    <div class="row center-block">
      <h2>Data tables</h2>
      <div class="col-md-12">
        <div class="box">
          <div class="box-header">
            <h3 class="box-title">Data Table With Full Features <span style="align:right" v-on:click="updateStudents"><i class="fa fa-refresh"></i>Refresh</span></h3>
          </div>
          <!-- /.box-header -->
          <div class="box-body">
            <div class="dataTables_wrapper form-inline dt-bootstrap" id="example1_wrapper">
              <div class="row">
                <div class="col-sm-6">
                  <div id="example1_length" class="dataTables_length">
                  </div>
                </div>
              </div>

              <div class="row">
                <div class="col-sm-12">
                  <table aria-describedby="example1_info" role="grid" id="example1" class="table table-bordered table-striped dataTable">
                    <thead>
                      <tr role="row">
                        <th aria-label="activate to sort column descending" aria-sort="ascending" style="width: 167px;" colspan="1" rowspan="1" aria-controls="example1" tabindex="0" class="sorting_asc" v-for="item in field_names" track-by="$index">{{item}}</th>                      </tr>
                    </thead>
                    <tbody>
                      <tr class="odd" role="row" v-for="line in table" track-by="$index">
                        <td v-for="item in line" track-by="$index">{{item}}</td>
                      </tr>
                    </tbody>
                    <tfoot>

                    </tfoot>
                  </table>
                </div>
              </div>
            </div>
            <!-- /.box-body -->
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import $ from 'jquery'

// Require needed datatables modules
require('datatables.net')
require('datatables.net-bs')

module.exports = {
  name: 'Students',
  ready: function () {
    $('#example1').DataTable()
  },
  methods: {
    updateStudents: function () {
      this.$parent.callAPI('GET', '/api/student', '').then(
        function (response) {
          if (response.data) {
            var data = response.data
            console.log(JSON.stringify(data))
          } else {
            console.log('timeout')
          }
        })
    }
  },
  data: function () {
    return {'table': [['John Doe', 'Male', '1996/03/27', 'Meh', 'Meh']],
            'field_names': ['中文名', '英文名', '生日', '', '']}
  }
}
</script>

<style>
</style>
