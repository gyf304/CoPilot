<template>
  <section class="content">
    <div class="row center-block">
      <h2>Data tables</h2>
      <div class="col-md-12">
        <div class="box">
          <div class="box-header">
            <h3 class="box-title" style="text-align: justify"><span style="width: 100%"></span><span ><i class="fa fa-refresh"></i>Refresh</span></h3>
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
                        <th aria-label="Rendering engine: activate to sort column descending" aria-sort="ascending" style="width: 167px;" colspan="1" rowspan="1" aria-controls="example1" tabindex="0" class="sorting_asc">Rendering engine</th>
                        <th aria-label="Browser: activate to sort column ascending" style="width: 207px;" colspan="1" rowspan="1" aria-controls="example1" tabindex="0" class="sorting">Browser</th>
                      </tr>
                    </thead>
                    <tbody>
                    </tbody>
                    <tfoot>
                      <tr>
                        <th colspan="1" rowspan="1">Rendering engine</th>
                        <th colspan="1" rowspan="1">Browser</th>
                      </tr>
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
    $('#example1').DataTable({
      'ajax': {
        'url': 'http://localhost:5000/api/student',
        'type': 'GET',
        'beforeSend': function (request) {
          request.setRequestHeader('Content-Type', 'application/vnd.api+json')
          request.setRequestHeader('Accept', 'application/vnd.api+json')
        }
      },
      'columns': [
        { 'data': 'chinese_name' },
        { 'data': 'english_name' }
      ]
    })
  },
  attached: function () {
    console.log('attached')
    // $('#example1').DataTable()
  },
  data: function () {
    return {'table': [['']],
            'fieldNames': ['中文名', '英文名'],
            'page': 1,
            'totalPages': 10}
  },
  methods: {
  }
}
</script>

<style>
</style>
