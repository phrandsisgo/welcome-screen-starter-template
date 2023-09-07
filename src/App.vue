<script>
export default {
  name: "App",
  data() {
    return {
      title: "Welcome to Opportunity",
      sheet_id: import.meta.env.VITE_GOOGLE_SHEET_ID,
      api_token: import.meta.env.VITE_GOOGLE_API_KEY,
     //api_token: "AIzaSyBSzduu2jm5uF3pCFYrv98YIrvFgSd5kXY",
     entries:[],
      cardItem : [
        {
          id: 1,
          date: '07.09.2023 , 14:00',
          title: 'Druckerpapier einkaufen',
          description: 'Da uns kürzlich die Druckerpatronen ausgegangen sind, müssen für die HR-Abteilung neue Druckerpatronen gekauft werden.',
        },
        {
          id: 2,
          date: '08.09.2023 , 10:30',
          title: 'Besprechung mit dem Vertriebsteam',
          description: 'Besprechung mit dem Vertriebsteam, um die Verkaufsstrategie für das kommende Quartal zu planen.',
        },
        {
          id: 3,
          date: '09.09.2023 , 16:15',
          title: 'Monatlicher Finanzbericht erstellen',
          description: 'Erstellung des monatlichen Finanzberichts für die Geschäftsführung und Analyse der finanziellen Leistung des Unternehmens.',
        },
        {
          id: 4,
          date: '10.09.2023 , 13:45',
          title: 'Kundengespräch mit XYZ Inc.',
          description: 'Telefonisches Gespräch mit dem Kunden XYZ Inc. bezüglich ihres laufenden Projekts und Klärung von offenen Fragen.',
        },
        {
          id: 5,
          date: '11.09.2023 , 09:00',

          title: 'Mitarbeitergespräche führen',
          description: 'Durchführung von jährlichen Mitarbeitergesprächen und Festlegung von Zielen für das kommende Jahr.',
        },
        {
          id: 6,

          date: '12.09.2023 , 15:30',
          title: 'Besprechung mit dem IT-Team',
          description: 'Besprechung mit dem IT-Team, um technische Anforderungen für das neue Projekt zu erörtern und Ressourcen zuzuweisen.',
        },
      ],
    
    };
  },
  computed: {
    gsheet_url() {
      return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
    }
  },
  mounted() {
    this.getData(); // get first initial data and then wait for the next update
  },
  methods: {
      async getData() {
        const response = await fetch(this.gsheet_url);
        const data = await response.json();
        this.entries = data.valueRanges[0].values;
        //console.log("this is the data" +JSON.stringify(data));
        console.log("this is the data" +this.entries);
      }
  },


};

const cardItem = [
  {
    id: 1,
    date: '07.09.2023 , 14:00',
    title: 'Druckerpapier einkaufen',
    description: 'Da uns kürzlich die Druckerpatronen ausgegangen sind, müssen für die HR-Abteilung neue Druckerpatronen gekauft werden.',
  },
  {
    id: 2,
    date: '08.09.2023 , 10:30',
    title: 'Besprechung mit dem Vertriebsteam',
    description: 'Besprechung mit dem Vertriebsteam, um die Verkaufsstrategie für das kommende Quartal zu planen.',
  },
  {
    id: 3,
    date: '09.09.2023 , 16:15',
    title: 'Monatlicher Finanzbericht erstellen',
    description: 'Erstellung des monatlichen Finanzberichts für die Geschäftsführung und Analyse der finanziellen Leistung des Unternehmens.',
  },
  {
    id: 4,
    date: '10.09.2023 , 13:45',
    title: 'Kundengespräch mit XYZ Inc.',
    description: 'Telefonisches Gespräch mit dem Kunden XYZ Inc. bezüglich ihres laufenden Projekts und Klärung von offenen Fragen.',
  },
  {
    id: 5,
    date: '11.09.2023 , 09:00',
    title: 'Mitarbeitergespräche führen',
    description: 'Durchführung von jährlichen Mitarbeitergesprächen und Festlegung von Zielen für das kommende Jahr.',
  },
  {
    id: 6,
    date: '12.09.2023 , 15:30',
    title: 'Besprechung mit dem IT-Team',
    description: 'Besprechung mit dem IT-Team, um technische Anforderungen für das neue Projekt zu erörtern und Ressourcen zuzuweisen.',
  },
];

</script>
<template>
  <div id="application">
    <h1 class="site-title">{{ title }}</h1>
    <h3 class="site-date">{{new Date().toLocaleDateString('en-GB').replace(/\//g, '.')}}</h3>
    <div class="card">
      <p class="timeStamp">14.00 Uhr</p>
      <p class="cardTitle">Projekt fertigstellen</p>
      <p class="cardBeschreibung"> Interesse für den zweiten Kurs werden uns besuchen</p>
    </div>

   

    <div class="card" v-for="card in cardItem">
      {{ card.id }}
      <p class="timeStamp">{{card.date}}</p>
      <p class="cardTitle"> {{ card.title }}</p>
      <p class="cardBeschreibung"> {{ card.description }}</p>

    </div>
    <div id="datenEinsicht" v-for="eintrag in entries">
      Hallo
    </div>
    <br><br><br>
  </div>
  <footer>
    <div id="footerLogos">
      <img src="src/assets/STZH_SEB_Logo.png" alt="Stadt Zürich Logo" class="logosSponsors">
      <img src="src/assets/Opportunity.png" alt="Opportunity Logo" class="logosSponsors">
      <img src="src/assets/SAG_Logo_De.png" alt="SAG-Logo" class="logosSponsors">
    </div>
  </footer>
</template>
<style>
#application {
  font-family: "Inter", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #323d4a;
  margin: 60px;
  background-color: lightcyan;
}
.card{
  background-color: darkblue;
  padding: 10px;
  margin-top: 15px;
}
.site-date{
  color: grey;
}
.timeStamp{
  color: tomato;
  font-weight: bold;
  font-size: large;
}
.cardTitle{
  color: lightsalmon;
  font-size: large;
  font-weight: bold;
}
.cardBeschreibung{
  color: lightcoral;
}
#footerLogos{
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  margin: 10px;
  color: darkblue;
}
.logosSponsors{
  width: 200px;
  height: 50px;
}
footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  background-color: white;
}
</style>
