

1. TeslaBlogger adinda bir blank solution açilir.

2. ASP.NET Core 3.1 Web Application (MVC) projesi eklenir.

	2.1. Views->Home klasorunun icindeki Index view'a request aticagimiz api için ajax ile Get() fonksiyonu yazilir ve gelen verileri dolduracagimiz html kodlari yazilir.

	<div class=" row">
    <div class=" col-sm-12">
        <div class=" card">
            <div class="card-header">
                <h3 class="card-title">List of Article About Tesla</h3>
            </div>
            <div class="card-header">
                <input type="button" value="List of Article" class="btn btn-block btn-primary" onclick="Get()" />
            </div>
            <div class="card-body">
                <table class="table table-bordered table-sm">
                    <thead>
                        <tr>
                            <th>Author</th>
                            <th>Title</th>
                            <th>Content</th>
                        </tr>
                    </thead>
                    <tbody>                 
                    </tbody>
                </table>
          </div>
      </div>
   </div>
</div>

<script>
    function Get() {

        $.ajax({

            url: "http://newsapi.org/v2/everything?q=tesla&from=2021-01-23&sortBy=publishedAt&apiKey=467f8d2e2df54419a7d03fc35876e296",
            type: "GET",
            success: function (response) {
                calistir(response)
            }

        });

    }

    function calistir(data) {
        for (var i = 0; i < data.articles.length; i++) {
            var author = data.articles[i].author;
            var title = data.articles[i].title;
            var description = data.articles[i].description;

            var html = "";
            html += "<tr>";
            html += "<td>" + author + "</td>";
            html += "<td>" + title + "</td>";
            html += "<td>" + description + "</td>";
            html += "</tr>";
            $("table").append(html);
        }
    }
</script>

Projenin amaci : https://newsapi.org/ adresinden hazirlanmis olan api'lerden birine request atarak datalari "get" etmektir.Bu islemi ajax yöntemiyle gerçeklestiriyoruz.
