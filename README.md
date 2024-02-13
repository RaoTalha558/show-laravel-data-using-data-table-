# show-laravel-data-using-data-table-
Display laravel data using ajax and data table simple change tabel id and set in table, tables's id and set url route and ajax route 
and use cdn of dtaa table
this is my blade 
<table id="client_list_point" class="display table">
                        <thead>
                            <tr>
                                <th>ID</th>
                                <th>{{ __('Total Points') }}</th>
                                <th>{{ __('Remaining Points') }}</th>
                            </tr>
                        </thead>
                        <tbody>
                        </tbody>
                    </table>

and thsi is my script 
<script>
    $(document).ready(function() {
    $.ajax({
        url: '{{ route('clients.getPoints') }}',
        type: 'GET',
        success: function(data) {
            $('#client_list_point').DataTable({
                data: data,
                columns: [
                    { data: 'id' },
                    { data: 'total_user_point' },
                    { data: 'remaining_user_point' }
                ]
            });
        },
        error: function(error) {
            console.log(error);
        }
    });
});

</script>
this is my controller code 

public function getPoints()
  {
    $points = Point::with('Clients')->get();
    return response()->json($points);
  }

and here is my route 
 Route::get('clients/getPoints', 'PointController@getPoints')->name('clients.getPoints');
