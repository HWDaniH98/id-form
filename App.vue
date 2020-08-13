<template>
  <div id="app">
    <form>
      <!-- Selects country -->
      <select name="country" id="country" v-model="country">
        <option disabled>Select country/region</option>
        <option v-for="choice in idTypes" :key="choice.country">{{choice.country}}</option>
      </select>
      <!-- Selects form of ID -->
      <select name="type" id="type" v-model="idType">
        <option disabled>Select your form of ID</option>
        <option v-for="choice in ids" :key="choice">{{choice.name}}</option>
      </select>
      <!-- Records ID value -->
      <label for="id">{{ idType.name }}</label>
      <input type="text" id="id" v-model.trim="idNum">
    </form>
  </div>
</template>

<script>
  export default
  {
    name: 'App',
    data()
    {
      return {
        //Used to narrow down ID types by country
        country: "",
        idTypes:
        [
          {
            /*Albanian IDs*/
            country: "Albania",
            types:
            [
              {
                symbol: "AL",
                name: "Numri i Identitetit"
              }
            ]
          },
          {
            /*Argentinian IDs*/
            country: "Argentina",
            types:
            [
              {
                symbol: "DN",
                name: "Documento Nacional de Identidad"
              },
              {
                symbol: "CT",
                name: "Código Único de Identificación Tributaria"
              },
              {
                symbol: "CL",
                name: "Código de Identificación Laboral"
              }
            ]
          },
          {
            /*Austrian IDs*/
            country: "Austria",
            types:
            [
              {
                symbol: "AT",
                name: "Sector-Specific Personal Identifier"
              }
            ]
          },
          {
            /*Bahrain IDs*/
            country: "Bahrain",
            types:
            [
              {
                symbol: "BH",
                name: "الرقم الشخصي‎"
              }
            ]
          },
          {
            /*Belgian IDs*/
            name: "Belgium",
            types:
            [
              {
                symbol: "BE",
                name: "National Register Number"
              }
            ]
          },
          {
            /*Brazilian IDs*/
            country: "Brazil",
            types:
            [
              {
                symbol: "RG",
                name: "Registro Geral"
              },
              {
                symbol: "CP",
                name: "Cadastro de Pessoas Físicas"
              },
              {
                symbol: "SI",
                name: "Social Security Number"
              },
              {
                symbol: "EN",
                name: "Election Identification Number"
              }
            ]
          },
          {
            /*Chinese IDs*/
            country: "China",
            types:
            [
              {
                symbol: "CN",
                name: "Identity card number"
              }
            ]
          },
          {
            /*Chilean IDs*/
            country: "Chile",
            types:
            [
              {
                symbol: "CL",
                name: "Rol Único Nacional"
              }
            ]
          },
          {
            /*Colombian IDs*/
            country: "Colombia",
            types:
            [
              {
                symbol: "CC",
                name: "Cédula de ciudadanía",
              },
              {
                symbol: "TI",
                name: "Tarjeta de identidad",
              },
              {
                symbol: "NI",
                name: "Cédula de extranjería",
              },
              {
                symbol: "NU",
                name: "Número único de identificación personal",
              },
              {
                symbol: "RC",
                name: "Registro civil",
              },
              {
                symbol: "PA",
                name: "Pasaporte"
              }
            ]
          },
          {
            /*Croatian IDs*/
            country: "Croatia",
            types:
            [
              {
                symbol: "HR",
                name: "Osobni identifikacijski broj"
              }
            ]
          },
          {
            /*Czech IDs*/
            country: "Czechia",
            types:
            [
              {
                symbol: "CZ",
                name: "Rodné číslo"
              }
            ]
          },
          {
            /*Danish IDs*/
            country: "Denmark",
            types:
            [
              {
                symbol: "DK",
                name: "Centrale Personregister"
              }
            ]
          },
          {
            /*Estonian IDs*/
            country: "Estonia",
            types:
            [
              {
                symbol: "EE",
                name: "Isikukood"
              }
            ]
          },
          {
            /*Finnish IDs*/
            country: "Finland",
            types:
            [
              {
                symbol: "FI",
                name: "Henkilötunnus"
              }
            ]
          },
          {
            /*French IDs*/
            country: "France",
            types:
            [
              {
                symbol: "FR",
                name: "INSEE code"
              }
            ]
          },
          {
            /*Hong Kong IDs*/
            country: "Hong Kong",
            types:
            [
              {
                symbol: "HK",
                name: "HKID number"
              }
            ]
          },
          {
            /*Indian IDs*/
            country: "India",
            types:
            [
              {
                symbol: "PN",
                name: "Permanent account number"
              },
              {
                symbol: "AN",
                name: "Aadhaar number"
              }
            ]
          },
          {
            /*Indonesian IDs*/
            country: "Indonesia",
            types:
            [
              {
                symbol: "ID",
                name: "Nomor Induk Kependudukan"
              }
            ]
          },
          {
            /*Iranian IDs*/
            country: "Iran",
            types:
            [
              {
                symbol: "IR",
                name: "National Identification Number"
              }
            ]
          },
          {
            /*Israel IDs*/
            country: "Israel",
            types:
            [
              {
                symbol: "IL",
                name: "מספר זהות"
              }
            ]
          },
          {
            /*Italian IDs*/
            country: "Italy",
            types:
            [
              {
                symbol: "IT",
                name: "Codice fiscale"
              }
            ]
          },
          {
            /*Japanese IDs*/
            country: "Japan",
            types:
            [
              {
                symbol: "JP",
                name: "マイナンバー"
              }
            ]
          },
          {
            /*Kazakhstan*/
            country: "Kazakhstan",
            types:
            [
              {
                symbol: "KZ",
                name: "Individual Identification Number"
              }
            ]
          },
          {
            /*Malaysian IDs*/
            country: "Malaysia",
            types:
            [
              {
                symbol: "MY",
                name: "National Registration Identification Card Number"
              }
            ]
          },
          {
            /*Mexican IDs*/
            country: "Mexico",
            types:
            [
              {
                symbol: "CU",
                name: "Clave Única de Registro de Población"
              },
              {
                symbol: "RF",
                name: "Registro Federal del Contribuyente"
              }
            ]
          },
          {
            /*Dutch IDs*/
            country: "Netherlands",
            types:
            [
              {
                symbol: "NL",
                name: "Burgerservicenummer"
              }
            ]
          },
          {
            /*Nigerian IDs*/
            country: "Nigeria",
            types:
            [
              {
                symbol: "NG",
                name: "Nationial Identification Number"
              }
            ]
          },
          {
            /*Norway IDs*/
            country: "Norway",
            types:
            [
              {
                symbol: "NO",
                name: "Fødselsnummer"
              }
            ]
          },
          {
            /*Phillipino IDs*/
            country: "The Phillipines",
            types:
            [
              {
                symbol: "PH",
                name: "PhilSys number"
              }
            ]
          },
          {
            /*Polish IDs*/
            country: "Poland",
            types:
            [
              {
                symbol: "PL",
                name: "PESEL Number"
              }
            ]
          },
          {
            /*Portuguese IDs*/
            country: "Portugal",
            types:
            [
              {
                symbol: "NC",
                name: "Número de identificação civil"
              },
              {
                symbol: "NF",
                name: "Número de identificação fiscal"
              },
              {
                symbol: "NS",
                name: "Número de Segurança Social"
              },
              {
                symbol: "NA",
                name: "Número de utente da Saúde"
              },
              {
                symbol: "NE",
                name: "Número de eleitor"
              },
              {
                symbol: "ND",
                name: "Número de carta de condução"
              }
            ]
          },
          {
            /*Singaporean IDs*/
            country: "Singapore",
            types:
            [
              {
                symbol: "NR",
                name: "NRIC number"
              },
              {
                symbol: "FI",
                name: "Foreign Identification Number"
              }
            ]
          },
          {
            /*South African IDs*/
            country: "South Africa",
            types:
            [
              {
                symbol: "ZA",
                name: "Person Identification Number"
              }
            ]
          },
          {
            /*South Korean IDs*/
            country: "South Korea",
            types:
            [
              {
                symbol: "KR",
                name: "Resident registration number"
              }
            ]
          },
          {
            /*Taiwanese IDs*/
            country: "Taiwan",
            types:
            [
              {
                symbol: "TW",
                name: "National Identification number"
              }
            ]
          },
          {
            /*US IDs*/
            country: "United States",
            types:
            [
              {
                symbol: "SS",
                name: "Social Security Number",
              },
              {
                symbol: "TN",
                name: "Tax Identification Number"
              }
            ]
          },
          {
            /*Zimbabwe IDs*/
            country: "Zimbabwe",
            types:
            [
              {
                symbol: "ZW",
                name: "National ID Number"
              }
            ]
          }
        ],

        //Used to record the ID type and value
        idType: "",
        idNum: ""
      }
    },
    computed:
    {
      //Selects the set of IDs associated with the country you choose
      ids()
      {
        let options = [];
        for (let i = 0; i < this.idTypes.length; i++)
        {
          if (this.country === this.idTypes[i].country)
          {
            options = this.idTypes[i].types;
          }
        }
        return options;
      }
    }
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
