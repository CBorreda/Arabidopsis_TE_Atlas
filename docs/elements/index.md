# Per element data

Here I'll add a table per superfamily. Each table will contain the following.


<div id="item-table">Loading...</div>
<div id="item-details" style="margin-top: 2em;"></div>

<script>
// Wait for DOM to load (in case MkDocs theme delays it)
document.addEventListener("DOMContentLoaded", function () {
  fetch("entries/items.json")
    .then((response) => {
      if (!response.ok) throw new Error("JSON not found");
      return response.json();
    })
    .then((data) => {
      const tableDiv = document.getElementById("item-table");
      tableDiv.innerHTML = "";  // Clear "Loading..."

      const table = document.createElement("table");
      table.style.width = "100%";
      table.border = "1";

      const header = table.insertRow();
      header.innerHTML = "<th>Superfamily</th><th>Family</th><th>Element</th>";

      data.forEach((item) => {
        const row = table.insertRow();
        row.innerHTML = `
          <td>${item.transposon_superfamily}</td>
          <td>${item.transposon_family}</td>
          <td><a href="details.html?id=${item.te_id}">${item.te_id}</button></td>
        `;
      });

      tableDiv.appendChild(table);

    })
    .catch((err) => {
      document.getElementById("item-table").innerHTML =
        "Error loading data: " + err.message;
    });
});
</script>
