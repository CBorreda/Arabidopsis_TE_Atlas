# Per element data

The following list includes all TEs found to be expressed through long-read sequencing in *ddm1*, *ddm1rdr2* and *ddm1rdr6* mutants, grown under control conditions or subjected  to a heat stress or biotic stress using flagellin.

For each entry, the DNA sequence of each TE-gene and each annotated isoform is reported, together with the protein sequence of the first and the longest ORF on each sense (forward and reverse). 

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
      // table.style.width = "100%";
      table.border = "1";
  
      const header = table.insertRow();
      header.innerHTML = "<th>Superfamily</th><th>Family</th><th>Element</th><th>DAPseq peaks</th><th>Coding sequences and ORFs</th><th>Expression</th><th>Engaged in translation?</th><th>Detected by MS?</th>";

      data.forEach((item) => {
        const row = table.insertRow();
        const geneLinks = item.tegene.map(geneId => {
          return `<a href="expression_hm.html?id=${geneId}">${geneId}</a>`;
        }).join("<br>")
        const riboLinks = item.ribo.map(ribo => {
          return `${ribo}`;
        }).join("<br>")
        const massLinks = item.mass.map(mass => {
          return `${mass}`;
        }).join("<br>");
        row.innerHTML = `
          <td>${item.transposon_superfamily}</td>
          <td>${item.transposon_family}</td>
          <td>${item.te_id}</td>
          <td><a href="dapseq_hm.html?id=${item.te_id}">Peaks</button></td>
          <td><a href="details.html?id=${item.te_id}">FASTA</button></td>
          <td>${geneLinks}</td>
          <td>${riboLinks}</td>
          <td>${massLinks}</td>
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
