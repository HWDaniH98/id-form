<template>
  <div id="app">
    <form v-on:submit.prevent>
      <div>
        <!-- Selects country -->
        <select name="country" id="country" v-model="country">
          <option disabled>Select country/region</option>
          <option v-for="choice in idTypes" :key="choice" v-bind:value="choice">{{choice.country}}</option>
        </select>
        <!-- Selects form of ID -->
        <select name="type" id="type" v-model="idType">
          <option disabled>Select your form of ID</option>
          <option v-for="choice in ids" :key="choice">{{choice.name}}</option>
        </select>
        <!-- Records ID value -->
        <label for="id">{{ idType.name }}</label>
        <input type="text" id="id" v-model.trim="idNum">
      </div>

      <div>
        <label for="countryCode">Phone Number</label>
        <!-- Selects country code -->
        <select name = "countryCode" id = "countryCode" v-model="countryCode">
          <option disabled>Select country code</option>
          <option v-for="code in country.num" :key="code" v-bind:value="code">{{code}}</option>
        </select>
        <!-- Records intranational phone number -->
        <input type="text" id="localNum" v-model.number="localNum">
        <!-- Triggers a method which concatenates country code and number -->
        <button v-on:click="phoneNumber">Send</button>
      </div>
    </form>
    <!-- Displays input information -->
    <p v-if="phoneNum !== ''">Your ID is {{idNum}} and your phone number is {{phoneNum}}.</p>
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
            ],
            num: ["+355"]
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
            ],
            num: ["+54"]
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
            ],
            num: ["+43"]
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
            ],
            num: ["+973"]
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
            ],
            num: ["+32"]
          },
          {
            /*Bosnian IDs*/
            country: "Bosnia and Herzegovinia",
            types:
            [
              {
                symbol: "BA",
                name: "Jedinstveni matični broj građana"
              }
            ],
            num: ["+387"]
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
            ],
            num: ["+55"]
          },
          {
            /*Bulgarian IDs*/
            country: "Bulgaria",
            types:
            [
              {
                symbol: "BG",
                name: "Единен граждански номер"
              }
            ],
            num: ["+359"]
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
            ],
            num: ["+86"]
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
            ],
            num: ["+56"]
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
            ],
            num: ["+57"]
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
            ],
            num: ["+385"]
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
            ],
            num: ["+420"]
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
            ],
            num: ["+45"]
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
            ],
            num: ["+372"]
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
            ],
            num: ["+358"]
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
            ],
            num: ["+33"]
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
            ],
            num: ["+852"]
          },
          {
            /*Icelandic IDs*/
            country: "Iceland",
            types:
            [
              {
                symbol: "IS",
                name: "Kennitala"
              }
            ],
            num: ["+354"]
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
            ],
            num: ["+91"]
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
            ],
            num: ["+62"]
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
            ],
            num: ["+98"]
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
            ],
            num: ["+972"]
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
            ],
            num: ["+39"]
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
            ],
            num: ["+81"]
          },
          {
            /*Lithuanian IDs*/
            country: "Lithuania",
            types:
            [
              {
                symbol: "LT",
                name: "Asmens kodas"
              }
            ],
            num: ["+370"]
          },
          {
            /*Luxembourgish IDs*/
            country: "Luxembourg",
            types:
            [
              {
                symbol: "LU",
                name: "Identification code"
              }
            ],
            num: ["+352"]
          },
          {
            /*Kazakhstani IDs*/
            country: "Kazakhstan",
            types:
            [
              {
                symbol: "KZ",
                name: "Individual Identification Number"
              }
            ],
            num: ["+7", "+997"]
          },
          {
            /*Kuwaiti IDs*/
            country: "Kuwait",
            types:
            [
              {
                symbol: "KW",
                name: "الرقم المدني‎"
              }
            ],
            num: "+965"
          },
          {
            /*Macau IDs*/
            country: "Macau",
            types:
            [
              {
                symbol: "MO",
                name: "BIRP Identification Number"
              }
            ],
            num: ["+853"]
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
            ],
            num: ["+60"]
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
            ],
            num: ["+52"]
          },
          {
            /*Moldovan IDs*/
            country: "Moldova",
            types:
            [
              {
                symbol: "MD",
                name: "Personal Code"
              }
            ],
            num: ["+373"]
          },
          {
            /*Montenegrin IDs*/
            country: "Montenegro",
            types:
            [
              {
                symbol: "ME",
                name: "Jedinstveni matični broj građana"
              }
            ],
            num: ["+382"]
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
            ],
            num: ["+31"]
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
            ],
            num: ["+234"]
          },
          {
            /*North Macedonian IDs*/
            country: "North Macedonia",
            types:
            [
              {
                symbol: "MK",
                name: "Единствен матичен број на граѓанинот"
              }
            ],
            num: ["+389"]
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
            ],
            num: ["+47"]
          },
          {
            /*Pakistani IDs*/
            country: "Pakistan",
            types:
            [
              {
                symbol: "PK",
                name: "NIC number"
              }
            ],
            num: ["+92"]
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
            ],
            num: ["+63"]
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
            ],
            num: ["+48"]
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
            ],
            num: ["+351"]
          },
          {
            /*Romanian IDs*/
            country: "Romania",
            types:
            [
              {
                symbol: "RO",
                name: "Cod Numeric Personal"
              }
            ],
            num: ["+40"]
          },
          {
            /*IDs of San Marino*/
            country: "San Marino",
            types:
            [
              {
                symbol: "SM",
                name: "Codice ISS"
              }
            ],
            num: ["+378"]
          },
          {
            /*Serbian IDs*/
            country: "Serbia",
            types:
            [
              {
                symbol: "RS",
                name: "Јединствени матични број грађана"
              }
            ],
            num: ["+381"]
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
            ],
            num: ["+65"]
          },
          {
            /*Slovak IDs*/
            country: "Slovakia",
            types:
            [
              {
                symbol: "BN",
                name: "Rodné číslo"
              },
              {
                symbol: "AX",
                name: "Číslo občianskeho preukazu"
              }
            ],
            num: ["+421"]
          },
          {
            /*Slovene IDs*/
            country: "Slovenia",
            types:
            [
              {
                symbol: "SI",
                name: "Enotna matična številka občana"
              }
            ],
            num: ["+386"]
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
            ],
            num: ["+27"]
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
            ],
            num: ["+82"]
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
            ],
            num: ["+886"]
          },
          {
            /*Thai IDs*/
            country: "Thailand",
            types:
            [
              {
                symbol: "TH",
                name: "Population Identification Code"
              }
            ],
            num: ["+66"]
          },
          {
            /*UAE IDs*/
            country: "United Arab Emirates",
            types:
            [
              {
                symbol: "AE",
                name: "Identification Number"
              }
            ],
            num: ["+971"]
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
            ],
            num: ["+1"]
          },
          {
            /*Vietnamese IDs*/
            country: "Vietnam",
            types:
            [
              {
                symbol: "VN",
                name: "ID card number"
              }
            ],
            num: ["+84"]
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
            ],
            num: ["+263"]
          }
        ],

        //Used to record the ID type and value
        idType: "",
        idNum: "",

        //Used to record country code
        countryCode: "",
        /*countryCodes:
        [
          {
            name: "US or Canada (+1)",
            num: "+1"
          },
          {
            name: "Egypt (+20)",
            num: "+20"
          },
          {
            name: "South Africa (+27)",
            num: "+27"
          },
          {
            name: "South Sudan (+211)",
            num: "+211"
          },
          {
            name: "Morocco and/or Western Sahara (+212)",
            num: "+212"
          },
          {
            name: "Algeria (+213)",
            num: "+213"
          },
          {
            name: "Tunisia (+216)",
            num: "+216"
          },
          {
            name: "Libya (+218)",
            num: "+218"
          },
          {
            name: "The Gambia (+220)",
            num: "+220"
          },
          {
            name: "Senegal (+221)",
            num: "+221"
          },
          {
            name: "Mauritania (+222)",
            num: "+222"
          },
          {
            name: "Mali (+223)",
            num: "+223"
          },
          {
            name: "Guinea (+224)",
            num: "+224"
          },
          {
            name: "Ivory Coast (+225)",
            num: "+225"
          },
          {
            name: "Burkina Faso (+226)",
            num: "+226"
          },
          {
            name: "Niger (+227)",
            num: "+227"
          },
          {
            name: "Togo (+228)",
            num: "+228"
          },
          {
            name: "Benin (+229)",
            num: "+229"
          },
          {
            name: "Mauritius (+230)",
            num: "+230"
          },
          {
            name: "Liberia (+231)",
            num: "+231"
          },
          {
            name: "Sierra Leone (+232)",
            num: "+232"
          },
          {
            name: "Ghana (+233)",
            num: "+233"
          },
          {
            name: "Nigeria (+234)",
            num: "+234"
          },
          {
            name: "Chad (+235)",
            num: "+235"
          },
          {
            name: "Central African Republic (+236)",
            num: "+236"
          },
          {
            name: "Cameroon (+237)",
            num: "+237"
          },
          {
            name: "Cape Verde (+238)",
            num: "+238"
          },
          {
            name: "São Tomé and Príncipe (+239)",
            num: "+239"
          },
          {
            name: "Equatorial Guinea (+240)",
            num: "+240"
          },
          {
            name: "Gabon (+241)",
            num: "+241"
          },
          {
            name: "Republic of the Congo (+242)",
            num: "+242"
          },
          {
            name: "Democratic Republic of the Congo (+243)",
            num: "+243"
          },
          {
            name: "Angola (+244)",
            num: "+244"
          },
          {
            name: "Guinea-Bissau (+245)",
            num: "+245"
          },
          {
            name: "British Indian Ocean Territory (+246)",
            num: "+246"
          },
          {
            name: "🇦🇨 Ascension Island (+247)",
            num: "+247"
          },
          {
            name: "Seychelles (+248)",
            num: "+248"
          },
          {
            name: "Sudan (+249)",
            num: "+249"
          },
          {
            name: "Rwanda (+250)",
            num: "+250"
          },
          {
            name: "Ethiopia (+251)",
            num: "+251"
          },
          {
            name: "Somalia (+252)",
            num: "+252"
          },
          {
            name: "Djibouti (+253)",
            num: "+253"
          },
          {
            name: "Kenya (+254)",
            num: "+254"
          },
          {
            name: "Tanzania (+255)",
            num: "+255"
          },
          {
            name: "Uganda (+256)",
            num: "+256"
          },
          {
            name: "Burundi (+257)",
            num: "+257"
          },
          {
            name: "Mozambique (+258)",
            num: "+258"
          },
          {
            name: "Zambia (+260)",
            num: "+260"
          },
          {
            name: "Madagascar (+261)",
            num: "+261"
          },
          {
            name: "Mayotte, Réunion, or the French Southern and Antarctic Lands (+262)",
            num: "+262"
          },
          {
            name: "Zimbabwe (+263)",
            num: "+263"
          },
          {
            name: "Namibia (+264)",
            num: "+264"
          },
          {
            name: "Malawi (+265)",
            num: "+265"
          },
          {
            name: "Lesotho (+266)",
            num: "+266"
          },
          {
            name: "Botswana (+267)",
            num: "+267"
          },
          {
            name: "Eswatini (+268)",
            num: "+268"
          },
          {
            name: "Comoros (+269)",
            num: "+269"
          },
          {
            name: "Saint Helena or Tristan da Cunha (+290)",
            num: "+290"
          },
          {
            name: "Eritria (+291)",
            num: "+291"
          },
          {
            name: "Aruba (+297)",
            num: "+297"
          },
          {
            name: "Faroe Islands (+298)",
            num: "+298"
          },
          {
            name: "Greenland (+299)",
            num: "+299"
          },
          {
            name: "Greece (+30)",
            num: "+30"
          },
          {
            name: "Netherlands (+31)",
            num: "+31"
          },
          {
            name: "Belgium (+32)",
            num: "+32"
          },
          {
            name: "France (+33)",
            num: "+33"
          },
          {
            name: "Spain (+34)",
            num: "+34"
          },
          {
            name: "Hungary (+36)",
            num: "+36"
          },
          {
            name: "Italy or Vatican City (+39)",
            num: "+39"
          },
          {
            name: "Gibraltar (+350)",
            num: "+350"
          },
          {
            name: "Portugal (+351)",
            num: "+351"
          },
          {
            name: "Luxembourg (+352)",
            num: "+352"
          },
          {
            name: "Ireland (+353)",
            num: "+353"
          },
          {
            name: "Iceland (+354)",
            num: "+354"
          },
          {
            name: "Albania (+355)",
            num: "+355"
          },
          {
            name: "Malta (+356)",
            num: "+356"
          },
          {
            name: "Cyprus (+357)",
            num: "+357"
          },
          {
            name: "Finland or the Åland Islands (+358)",
            num: "+358"
          },
          {
            name: "Bulgaria (+359)",
            num: "+359"
          },
          {
            name: "Lithuania (+370)",
            num: "+370"
          },
          {
            name: "Latvia (+371)",
            num: "+371"
          },
          {
            name: "Estonia (+372)",
            num: "+372"
          },
          {
            name: "Moldova (+373)",
            num: "+373"
          },
          {
            name: "Armenia (+374)",
            num: "+374"
          },
          {
            name: "Belarus (+375)",
            num: "+375"
          },
          {
            name: "🇦🇩 Andorra (+376)",
            num: "+376"
          },
          {
            name: "Monaco (+377)",
            num: "+377"
          },
          {
            name: "San Marino (+378)",
            num: "+378"
          },
          {
            name: "Vatican City (+379)",
            num: "+379"
          },
          {
            name: "Ukraine (+380)",
            num: "+380"
          },
          {
            name: "Serbia (+381)",
            num: "+381"
          },
          {
            name: "Montenegro (+382)",
            num: "+382"
          },
          {
            name: "Kosovo (+383)",
            num: "+383"
          },
          {
            name: "Croatia (+385)",
            num: "+385"
          },
          {
            name: "Slovenia (+386)",
            num: "+386"
          },
          {
            name: "Bosnia and Herzegovinia (+387)",
            num: "+387"
          },
          {
            name: "North Macedonia (+389)",
            num: "+389"
          },
          {
            name: "Romania (+40)",
            num: "+40"
          },
          {
            name: "Switzerland (+41)",
            num: "+41"
          },
          {
            name: "Austria (+43)",
            num: "+43"
          },
          {
            name: "United Kingdom, Gurnsey, Isles of Man, or Jersey (+44)",
            num: "+44"
          },
          {
            name: "Denmark (+45)",
            num: "+45"
          },
          {
            name: "Sweden (+46)",
            num: "+46"
          },
          {
            name: "Norway, Svalbard, Jan Mayen, or Bouvet Island (+47)",
            num: "+47"
          },
          {
            name: "Poland (+48)",
            num: "+48"
          },
          {
            name: "Germany (+49)",
            num: "+49"
          },
          {
            name: "Czechia (+420)",
            num: "+420"
          },
          {
            name: "Slovakia (+421)",
            num: "+421"
          },
          {
            name: "Liechtenstein (+423)",
            num: "+423"
          },
          {
            name: "Peru (+51)",
            num: "+51"
          },
          {
            name: "Mexico (+52)",
            num: "+52"
          },
          {
            name: "Cuba (+53)",
            num: "+53"
          },
          {
            name: "Argentina (+54)",
            num: "+54"
          },
          {
            name: "Brazil (+55)",
            num: "+55"
          },
          {
            name: "Chile (+56)",
            num: "+56"
          },
          {
            name: "Colombia (+57)",
            num: "+57"
          },
          {
            name: "Venezuela (+58)",
            num: "+58"
          },
          {
            name: "Falkland Islands or South Georgia and the South Sandwich Islands (+500)",
            num: "+500"
          },
          {
            name: "Belize (+501)",
            num: "+501"
          },
          {
            name: "Guatemala (+502)",
            num: "+502"
          },
          {
            name: "El Salvador (+503)",
            num: "+503"
          },
          {
            name: "Honduras (+504)",
            num: "+504"
          },
          {
            name: "Nicaragua (+505)",
            num: "+505"
          },
          {
            name: "Costa Rica (+506)",
            num: "+506"
          },
          {
            name: "Panama (+507)",
            num: "+507"
          },
          {
            name: "Saint Pierre and Miquelon (+508)",
            num: "+508"
          },
          {
            name: "Haiti (+509)",
            num: "+509"
          },
          {
            name: "Guadeloupe, Saint Barthélemy, or Saint Martin (+590)",
            num: "+590"
          },
          {
            name: "Bolivia (+591)",
            num: "+591"
          },
          {
            name: "Guyana (+592)",
            num: "+592"
          },
          {
            name: "Ecuador (+593)",
            num: "+593"
          },
          {
            name: "French Guiana (+594)",
            num: "+594"
          },
          {
            name: "Paraguay (+595)",
            num: "+595"
          },
          {
            name: "Martinique (+596)",
            num: "+596"
          },
          {
            name: "Suriname (+597)",
            num: "+597"
          },
          {
            name: "Uruguay (+598)",
            num: "+598"
          },
          {
            name: "Curaçao or the Carribean Netherlands (+599)",
            num: "+599"
          },
          {
            name: "Malaysia (+60)",
            num: "+60"
          },
          {
            name: "Australia, Christmas Island, or the Cocos Islands (+61)",
            num: "+61"
          },
          {
            name: "Indonesia (+62)",
            num: "+62"
          },
          {
            name: "Philippines (+63)",
            num: "+63"
          },
          {
            name: "New Zealand or the Pitcairn Islands (+64)",
            num: "+64"
          },
          {
            name: "Singapore (+65)",
            num: "+65"
          },
          {
            name: "Thailand (+66)",
            num: "+66"
          },
          {
            name: "Timor-Leste (+670)",
            num: "+670"
          },
          {
            name: "Norfolk Island, Australian Anarctic Territory, or Heard Island and McDonald Islands (+672)",
            num: "+672"
          },
          {
            name: "Brunei (+673)",
            num: "+673"
          },
          {
            name: "Nauru (+674)",
            num: "+674"
          },
          {
            name: "Papua New Guinea (+675)",
            num: "+675"
          },
          {
            name: "Tonga (+676)",
            num: "+676"
          },
          {
            name: "Solomon Islands (+677)",
            num: "+677"
          },
          {
            name: "Vanuatu (+678)",
            num: "+678"
          },
          {
            name: "Fiji (+679)",
            num: "+679"
          },
          {
            name: "Palau (+680)",
            num: "+680"
          },
          {
            name: "Wallis and Futuna (+681)",
            num: "+681"
          },
          {
            name: "Cook Islands (+682)",
            num: "+682"
          },
          {
            name: "Niue (+683)",
            num: "+683"
          },
          {
            name: "Samoa (+685)",
            num: "+685"
          },
          {
            name: "Kirbati (+686)",
            num: "+686"
          },
          {
            name: "New Caledonia (+687)",
            num: "+687"
          },
          {
            name: "Tuvalu (+688)",
            num: "+688"
          },
          {
            name: "French Polynesia (+689)",
            num: "+689"
          },
          {
            name: "Tokelau (+690)",
            num: "+690"
          },
          {
            name: "Federated States of Micronesia (+691)",
            num: "+691"
          },
          {
            name: "Marshall Islands (+692)",
            num: "+692"
          },
          {
            name: "Russia or Kazakhstan (+7)",
            num: "+7"
          },
          {
            name: "Japan (+81)",
            num: "+81"
          },
          {
            name: "South Korea (+82)",
            num: "+82"
          },
          {
            name: "Vietnam (+84)",
            num: "+84"
          },
          {
            name: "China (+86)",
            num: "+86"
          },
          {
            name: "North Korea (+850)",
            num: "+850"
          },
          {
            name: "Hong Kong (+852)",
            num: "+852"
          },
          {
            name: "Macau (+853)",
            num: "+853"
          },
          {
            name: "Cambodia (+855)",
            num: "+855"
          },
          {
            name: "Laos (+856)",
            num: "+856"
          },
          {
            name: "Bangladesh (+880)",
            num: "+880"
          },
          {
            name: "Taiwan (+886)",
            num: "+886"
          },
          {
            name: "Turkey or Northern Cyprus (+90)",
            num: "+90"
          },
          {
            name: "India (+91)",
            num: "+91"
          },
          {
            name: "Pakistan (+92)",
            num: "+92"
          },
          {
            name: "Afghanistan (+93)",
            num: "+93"
          },
          {
            name: "Sri Lanka (+94)",
            num: "+94"
          },
          {
            name: "Myanmar (+95)",
            num: "+95"
          },
          {
            name: "Iran (+98)",
            num: "+98"
          },
          {
            name: "Maldives (+960)",
            num: "+960"
          },
          {
            name: "Lebanon (+961)",
            num: "+961"
          },
          {
            name: "Jordan (+962)",
            num: "+962"
          },
          {
            name: "Syria (+963)",
            num: "+963"
          },
          {
            name: "Iraq (+964)",
            num: "+964"
          },
          {
            name: "Kuwait (+965)",
            num: "+965"
          },
          {
            name: "Saudi Arabia (+966)",
            num: "+966"
          },
          {
            name: "Yemen (+967)",
            num: "+967"
          },
          {
            name: "Oman (+968)",
            num: "+968"
          },
          {
            name: "Palestine (+970)",
            num: "+970"
          },
          {
            name: "United Arab Emirates (+971)",
            num: "+971"
          },
          {
            name: "Israel (+972)",
            num: "+972"
          },
          {
            name: "Bahrain (+973)",
            num: "+973"
          },
          {
            name: "Qatar (+974)",
            num: "+974"
          },
          {
            name: "Bhutan (+975)",
            num: "+975"
          },
          {
            name: "Mongolia (+976)",
            num: "+976"
          },
          {
            name: "Nepal (+977)",
            num: "+977"
          },
          {
            name: "Tajikistan (+992)",
            num: "+992"
          },
          {
            name: "Turkmenistan (+993)",
            num: "+993"
          },
          {
            name: "Azerbaijian (+994)",
            num: "+994"
          },
          {
            name: "Georgia (+995)",
            num: "+995"
          },
          {
            name: "Kyrgyzstan (+996)",
            num: "+996"
          },
          {
            name: "Kazakhstan (+997)",
            num: "+997"
          },
          {
            name: "Uzbekistan (+998)",
            num: "+998"
          }
        ],*/

        //Used to record phone numbers
        localNum: "", //Intranational number
        phoneNum: "" //International number
      }
    },
    computed:
    {
      //Selects the set of IDs associated with the country you choose
      ids()
      {
        let options = this.country.types;
        /*for (let i = 0; i < this.idTypes.length; i++)
        {
          if (this.country === this.idTypes[i].country)
          {
            options = this.idTypes[i].types;
          }
        }*/
        return options;
      }
    },
    methods:
    {
      //Records international phone number
      phoneNumber()
      {
        this.phoneNum = this.countryCode + this.localNum.toString();
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
