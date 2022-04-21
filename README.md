Use Chartjs in laravel-admin
======

[DEMO](http://demo.laravel-admin.org/chartjs)

Login using `admin/admin`

## Screenshot

![qq20180917-132122](https://user-images.githubusercontent.com/1479100/45607189-2b018b80-ba7d-11e8-845e-d7ab810bc07f.png)

## Installation

```bash
composer require snowsoft/chartjs

php artisan vendor:publish --tag=laravel-admin-chartjs
```

## Configuration

Open `config/admin.php`, add configurations that belong to this extension at `extensions` section.

```php

    'extensions' => [

        'chartjs' => [
        
            // Set to `false` if you want to disable this extension
            'enable' => true,
        ]
    ]

```

## Usage

Create a view in views directory like `resources/views/admin/chartjs.blade.php`, and add following codes:
```html
<canvas id="myChart" width="400" height="400"></canvas>
<script>
$(function () {
    var ctx = document.getElementById("myChart").getContext('2d');
    var myChart = new Chart(ctx, {
        type: 'bar',
        data: {
            labels: ["Red", "Blue", "Yellow", "Green", "Purple", "Orange"],
            datasets: [{
                label: '# of Votes',
                data: [12, 19, 3, 5, 2, 3],
                backgroundColor: [
                    'rgba(255, 99, 132, 0.2)',
                    'rgba(54, 162, 235, 0.2)',
                    'rgba(255, 206, 86, 0.2)',
                    'rgba(75, 192, 192, 0.2)',
                    'rgba(153, 102, 255, 0.2)',
                    'rgba(255, 159, 64, 0.2)'
                ],
                borderColor: [
                    'rgba(255,99,132,1)',
                    'rgba(54, 162, 235, 1)',
                    'rgba(255, 206, 86, 1)',
                    'rgba(75, 192, 192, 1)',
                    'rgba(153, 102, 255, 1)',
                    'rgba(255, 159, 64, 1)'
                ],
                borderWidth: 1
            }]
        },
        options: {
            scales: {
                yAxes: [{
                    ticks: {
                        beginAtZero:true
                    }
                }]
            }
        }
    });
});
</script>

```

Then show it on the page

```php
class ChartjsController extends Controller
{
    public function index(Content $content)
    {
        return $content
            ->header('Chartjs')
            ->body(new Box('Bar chart', view('admin.chartjs')));
    }
}
```

For more usage, please refer to the official [documentation](http://www.chartjs.org/) of chartjs.
  

License
------------
Licensed under [The MIT License (MIT)](LICENSE).
