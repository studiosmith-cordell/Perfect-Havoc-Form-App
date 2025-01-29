<script>
    import { quartOut } from 'svelte/easing';
    import { fade, slide } from 'svelte/transition';

    /** @type { string } */
    let firstName = $state(),
        /** @type { string } */
        lastName = $state(),
        /** @type { string } */
        companyName = $state(),
        /** @type { string } */
        artistName = $state(),
        /** @type { string } */
        email = $state(),
        /** @type { string } */
        phone = $state(),
        /** @type { string } */
        address = $state(),
        /** @type { string } */
        city = $state(),
        /** @type { string } */
        stateOrProvince = $state(),
        /** @type { string } */
        postcode = $state(),
        /** @type { string } */
        country = $state(),
        /** @type { boolean } */
        vat = $state(false),
        /** @type { string | undefined } */
        vatNumber = $state(),
        /** @type { boolean } */
        submitting = $state(false),
        /** @type { string | undefined }*/
        iframeUrl = $state(),
        /** @type { string | undefined }*/
        error = $state();

    /** @param { Event } e */
    async function handleFormSubmit(e) {
        e.preventDefault();
        submitting = true;

        const body = {
            firstName: firstName,
            lastName: lastName,
            companyName: companyName,
            artistName: artistName,
            email: email,
            phone: phone,
            address: address,
            city: city,
            stateOrProvince: stateOrProvince,
            postcode: postcode,
            country: country,
            vatNumber: vatNumber,
        };

        const request = await fetch(
            'https://curve.perfecthavoc.workers.dev/payee',
            {
                method: 'POST',
                body: JSON.stringify(body),
            }
        ).then((x) => x.json());

        if (request.error) {
            submitting = false;
            error = request.error;
            return;
        }

        iframeUrl = request.url;

        submitting = false;
    }
</script>

<div id="wrapper">
    {#if !iframeUrl}
        <form
            onsubmit={(e) => handleFormSubmit(e)}
            autocomplete="on"
        >
            <input
                bind:value={firstName}
                type="text"
                name="first-name"
                placeholder="First Name"
                required
                aria-required="true"
                aria-label="First Name"
                autocomplete="given-name"
            />

            <input
                bind:value={lastName}
                type="text"
                name="last-name"
                placeholder="Last Name"
                required
                aria-required="true"
                aria-label="Last Name"
                autocomplete="family-name"
            />

            <input
                bind:value={companyName}
                type="text"
                name="company-name"
                placeholder="Company (if applicable)"
                aria-label="Company (if applicable)"
                autocomplete="organization"
            />

            <input
                bind:value={artistName}
                type="text"
                name="artist-name"
                placeholder="Artist Name"
                required
                aria-required="true"
                aria-label="Artist Name"
            />

            <input
                bind:value={email}
                type="email"
                name="email"
                placeholder="Email"
                required
                aria-required="true"
                aria-label="Email"
                autocomplete="email"
            />

            <input
                bind:value={phone}
                type="tel"
                name="phone"
                placeholder="Phone"
                required
                aria-required="true"
                aria-label="Phone"
                autocomplete="tel"
            />

            <input
                bind:value={address}
                name="address"
                type="text"
                placeholder="Street Address"
                required
                aria-required="true"
                aria-label="Street Address"
                autocomplete="street-address"
            />

            <input
                bind:value={city}
                type="text"
                name="city"
                placeholder="City"
                required
                aria-required="true"
                aria-label="City"
                autocomplete="address-level2"
            />

            <input
                bind:value={stateOrProvince}
                type="text"
                name="state"
                placeholder="State/Province"
                aria-label="State or Province"
                autocomplete="address-level1"
            />

            <input
                bind:value={postcode}
                type="text"
                name="postcode"
                placeholder="Postcode"
                required
                aria-required="true"
                aria-label="Postcode"
                autocomplete="postal-code"
            />

            <select
                bind:value={country}
                id="country"
                name="country"
                required
                aria-required="true"
                aria-label="Country"
                autocomplete="country"
            >
                <option
                    selected
                    disabled
                    value=""
                >
                    Select Country
                </option>
                <option value="GB">United Kingdom</option>
                <option value="US">United States of America</option>
                <hr />
                <option value="AF">Afghanistan</option>
                <option value="AL">Albania</option>
                <option value="DZ">Algeria</option>
                <option value="AS">American Samoa</option>
                <option value="AD">Andorra</option>
                <option value="AO">Angola</option>
                <option value="AI">Anguilla</option>
                <option value="AQ">Antarctica</option>
                <option value="AG">Antigua and Barbuda</option>
                <option value="AR">Argentina</option>
                <option value="AM">Armenia</option>
                <option value="AW">Aruba</option>
                <option value="AU">Ashmore and Cartier Islands</option>
                <option value="AU">Australia</option>
                <option value="AT">Austria</option>
                <option value="AZ">Azerbaijan</option>
                <option value="BS">Bahamas</option>
                <option value="BH">Bahrain</option>
                <option value="BD">Bangladesh</option>
                <option value="BB">Barbados</option>
                <option value="BY">Belarus</option>
                <option value="BE">Belgium</option>
                <option value="BZ">Belize</option>
                <option value="BJ">Benin</option>
                <option value="BM">Bermuda</option>
                <option value="BT">Bhutan</option>
                <option value="BO">Bolivia</option>
                <option value="BA">Bosnia and Herzegovina</option>
                <option value="BW">Botswana</option>
                <option value="BV">Bouvet Island</option>
                <option value="BR">Brazil</option>
                <option value="IO">British Indian Ocean Territory</option>
                <option value="VG">British Virgin Islands</option>
                <option value="BN">Brunei</option>
                <option value="BG">Bulgaria</option>
                <option value="BF">Burkina Faso</option>
                <option value="BI">Burundi</option>
                <option value="CV">Cabo Verde</option>
                <option value="KH">Cambodia</option>
                <option value="CM">Cameroon</option>
                <option value="CA">Canada</option>
                <option value="KY">Cayman Islands</option>
                <option value="CF">Central African Republic</option>
                <option value="TD">Chad</option>
                <option value="CL">Chile</option>
                <option value="CN">China</option>
                <option value="CX">Christmas Island</option>
                <option value="CC">Cocos (Keeling) Islands</option>
                <option value="CO">Colombia</option>
                <option value="KM">Comoros</option>
                <option value="CD">Congo</option>
                <option value="CD">Democratic Republic of the Congo</option>
                <option value="CK">Cook Islands</option>
                <option value="AU">Coral Sea Islands</option>
                <option value="CR">Costa Rica</option>
                <option value="CI">Côte d'Ivoire</option>
                <option value="HR">Croatia</option>
                <option value="CU">Cuba</option>
                <option value="CY">Cyprus</option>
                <option value="CZ">Czech Republic</option>
                <option value="DK">Denmark</option>
                <option value="DJ">Djibouti</option>
                <option value="DM">Dominica</option>
                <option value="DO">Dominican Republic</option>
                <option value="EC">Ecuador</option>
                <option value="EG">Egypt</option>
                <option value="SV">El Salvador</option>
                <option value="GQ">Equatorial Guinea</option>
                <option value="ER">Eritrea</option>
                <option value="EE">Estonia</option>
                <option value="SZ">Eswatini</option>
                <option value="ET">Ethiopia</option>
                <option value="FK">Falkland Islands (Islas Malvinas)</option>
                <option value="FO">Faroe Islands</option>
                <option value="FJ">Fiji</option>
                <option value="FI">Finland</option>
                <option value="FR">France</option>
                <option value="GF">French Guiana</option>
                <option value="PF">French Polynesia</option>
                <option value="TF">French Southern and Antarctic Lands</option>
                <option value="GA">Gabon</option>
                <option value="GM">Gambia</option>
                <option value="GE">Georgia</option>
                <option value="DE">Germany</option>
                <option value="GH">Ghana</option>
                <option value="GI">Gibraltar</option>
                <option value="GR">Greece</option>
                <option value="GL">Greenland</option>
                <option value="GD">Grenada</option>
                <option value="GP">Guadeloupe</option>
                <option value="GU">Guam</option>
                <option value="GT">Guatemala</option>
                <option value="GG">Guernsey</option>
                <option value="GN">Guinea</option>
                <option value="GW">Guinea-Bissau</option>
                <option value="GY">Guyana</option>
                <option value="HT">Haiti</option>
                <option value="HM">Heard Island and McDonald Islands</option>
                <option value="VA">Holy See (Vatican City)</option>
                <option value="HN">Honduras</option>
                <option value="HK">Hong Kong</option>
                <option value="HU">Hungary</option>
                <option value="IS">Iceland</option>
                <option value="IN">India</option>
                <option value="ID">Indonesia</option>
                <option value="IR">Iran</option>
                <option value="IQ">Iraq</option>
                <option value="IE">Ireland</option>
                <option value="IM">Isle of Man</option>
                <option value="IL">Israel</option>
                <option value="IT">Italy</option>
                <option value="JM">Jamaica</option>
                <option value="SJ">Jan Mayen</option>
                <option value="JP">Japan</option>
                <option value="JE">Jersey</option>
                <option value="JO">Jordan</option>
                <option value="KZ">Kazakhstan</option>
                <option value="KE">Kenya</option>
                <option value="KI">Kiribati</option>
                <option value="KP">Korea, North</option>
                <option value="KR">Korea, South</option>
                <option value="KW">Kuwait</option>
                <option value="KG">Kyrgyzstan</option>
                <option value="LA">Laos</option>
                <option value="LV">Latvia</option>
                <option value="LB">Lebanon</option>
                <option value="LS">Lesotho</option>
                <option value="LR">Liberia</option>
                <option value="LY">Libya</option>
                <option value="LI">Liechtenstein</option>
                <option value="LT">Lithuania</option>
                <option value="LU">Luxembourg</option>
                <option value="MO">Macau</option>
                <option value="MK">Macedonia</option>
                <option value="MG">Madagascar</option>
                <option value="MW">Malawi</option>
                <option value="MY">Malaysia</option>
                <option value="MV">Maldives</option>
                <option value="ML">Mali</option>
                <option value="MT">Malta</option>
                <option value="MH">Marshall Islands</option>
                <option value="MQ">Martinique</option>
                <option value="MR">Mauritania</option>
                <option value="MU">Mauritius</option>
                <option value="YT">Mayotte</option>
                <option value="MX">Mexico</option>
                <option value="FM">Micronesia</option>
                <option value="MD">Moldova</option>
                <option value="MC">Monaco</option>
                <option value="MN">Mongolia</option>
                <option value="ME">Montenegro</option>
                <option value="MS">Montserrat</option>
                <option value="MA">Morocco</option>
                <option value="MZ">Mozambique</option>
                <option value="MM">Myanmar</option>
                <option value="NA">Namibia</option>
                <option value="NR">Nauru</option>
                <option value="UM">Navassa Island</option>
                <option value="NP">Nepal</option>
                <option value="NL">Netherlands</option>
                <option value="NC">New Caledonia</option>
                <option value="NZ">New Zealand</option>
                <option value="NI">Nicaragua</option>
                <option value="NE">Niger</option>
                <option value="NG">Nigeria</option>
                <option value="NU">Niue</option>
                <option value="NF">Norfolk Island</option>
                <option value="MP">Northern Mariana Islands</option>
                <option value="NO">Norway</option>
                <option value="OM">Oman</option>
                <option value="PK">Pakistan</option>
                <option value="PW">Palau</option>
                <option value="PS">Palestine</option>
                <option value="PA">Panama</option>
                <option value="PG">Papua New Guinea</option>
                <option value="PY">Paraguay</option>
                <option value="PE">Peru</option>
                <option value="PH">Philippines</option>
                <option value="PN">Pitcairn Islands</option>
                <option value="PL">Poland</option>
                <option value="PT">Portugal</option>
                <option value="PR">Puerto Rico</option>
                <option value="QA">Qatar</option>
                <option value="RE">Réunion</option>
                <option value="RO">Romania</option>
                <option value="RU">Russia</option>
                <option value="RW">Rwanda</option>
                <option value="SH">Saint Helena</option>
                <option value="KN">Saint Kitts and Nevis</option>
                <option value="LC">Saint Lucia</option>
                <option value="PM">Saint Pierre and Miquelon</option>
                <option value="VC">Saint Vincent and the Grenadines</option>
                <option value="WS">Samoa</option>
                <option value="SM">San Marino</option>
                <option value="ST">Sao Tome and Principe</option>
                <option value="SA">Saudi Arabia</option>
                <option value="SN">Senegal</option>
                <option value="RS">Serbia</option>
                <option value="SC">Seychelles</option>
                <option value="SL">Sierra Leone</option>
                <option value="SG">Singapore</option>
                <option value="SK">Slovakia</option>
                <option value="SI">Slovenia</option>
                <option value="SB">Solomon Islands</option>
                <option value="SO">Somalia</option>
                <option value="ZA">South Africa</option>
                <option value="GS"
                    >South Georgia and the South Sandwich Islands</option
                >
                <option value="ES">Spain</option>
                <option value="LK">Sri Lanka</option>
                <option value="SD">Sudan</option>
                <option value="SR">Suriname</option>
                <option value="SJ">Svalbard</option>
                <option value="SE">Sweden</option>
                <option value="CH">Switzerland</option>
                <option value="SY">Syria</option>
                <option value="TW">Taiwan</option>
                <option value="TJ">Tajikistan</option>
                <option value="TZ">Tanzania</option>
                <option value="TH">Thailand</option>
                <option value="TL">Timor-Leste</option>
                <option value="TG">Togo</option>
                <option value="TK">Tokelau</option>
                <option value="TO">Tonga</option>
                <option value="TT">Trinidad and Tobago</option>
                <option value="TN">Tunisia</option>
                <option value="TR">Turkey</option>
                <option value="TM">Turkmenistan</option>
                <option value="TC">Turks and Caicos Islands</option>
                <option value="TV">Tuvalu</option>
                <option value="UG">Uganda</option>
                <option value="UA">Ukraine</option>
                <option value="AE">United Arab Emirates</option>
                <option value="UY">Uruguay</option>
                <option value="UZ">Uzbekistan</option>
                <option value="VU">Vanuatu</option>
                <option value="VE">Venezuela</option>
                <option value="VN">Vietnam</option>
                <option value="VG">Virgin Islands</option>
                <option value="UM">Wake Island</option>
                <option value="WF">Wallis and Futuna</option>
                <option value="EH">Western Sahara</option>
                <option value="YE">Yemen</option>
                <option value="ZM">Zambia</option>
                <option value="ZW">Zimbabwe</option>
            </select>

            <div style="margin-block-start: 1em;">Are you VAT registered?</div>
            <div id="vat">
                <label>
                    <input
                        bind:group={vat}
                        type="radio"
                        name="vat"
                        value={true}
                        aria-label="I/We are VAT registered"
                    />
                    Yes
                </label>
                <label>
                    <input
                        bind:group={vat}
                        type="radio"
                        name="vat"
                        value={false}
                        aria-label="I/we are not VAT registered"
                    />
                    No
                </label>
            </div>

            {#if vat}
                <div in:fade={{ duration: 400, easing: quartOut }}>
                    <input
                        bind:value={vatNumber}
                        type="text"
                        name="vat-number"
                        placeholder="VAT Number"
                        required
                        aria-required="true"
                        aria-label="VAT Number"
                    />
                    <p>
                        If you deregister for VAT or the VAT registration above
                        is no longer applicable you must advise Perfect Havoc
                        Limited immediately in writing via email at <a
                            href="mailto:info@perfecthavoc.com"
                            >info@perfecthavoc.com</a
                        >.
                    </p>
                </div>
            {/if}

            <div style="margin-block-start: 1em;">
                <strong
                    >Please read and accept the below terms carefully:</strong
                >
            </div>

            <label>
                <input
                    type="checkbox"
                    name="details-true"
                    required
                    aria-required="true"
                />
                I/We confirm that the above details are correct.
            </label>

            <label>
                <input
                    type="checkbox"
                    name="amend"
                    required
                    aria-required="true"
                />
                I/We have the necessary authority to amend the above details and
                these details as amended above are correct.
            </label>

            <label>
                <input
                    type="checkbox"
                    name=""
                    required
                    aria-required="true"
                />
                I/We confirm that I/we agree to be covered by the Self-Billing system
                as detailed in our
                <a
                    href="http://perfecthavoc.com/terms-and-conditions/standard-payment-conditions"
                    >standard payment conditions</a
                >.
            </label>

            <button
                class:submitting
                aria-label="Next Step"
            >
                {#if submitting}
                    <span class="spinner"></span>
                {:else}
                    <span>Next</span>
                {/if}
            </button>
            {#if error}
                <span
                    transition:slide={{ duration: 400, easing: quartOut }}
                    style="margin-block-start: 0.5em; color: #f60000;"
                    >{error}</span
                >
            {/if}
        </form>
    {:else}
        <iframe
            in:fade={{ duration: 600, easing: quartOut }}
            title="Payee Form"
            src={iframeUrl}
        ></iframe>
    {/if}
</div>

<style>
    #wrapper {
        box-sizing: border-box;
        color: white;
        background-color: black;
        font-family: Inter, sans-serif;
        font-size: 1em;
        line-height: 1.25;
    }

    a {
        color: currentColor;
    }

    form {
        display: flex;
        flex-direction: column;
        gap: 1em;
        accent-color: #4ab9e9;
    }

    input,
    select {
        padding-block: 0.5em;
        font-size: 1em;
        color: white;
        background-color: transparent;
        border: none;
        border-bottom: solid 1px;
        outline: none;
        border-radius: 0;
    }

    input::placeholder {
        color: #a9a9a9;
    }

    input:focus {
        border-color: rgb(74, 185, 233);
    }

    select {
        cursor: pointer;
    }

    select:not(:user-valid) {
        color: #a9a9a9;
    }

    input[type='text'] {
        width: 100%;
    }

    input[type='radio'] {
        cursor: pointer;
    }

    #vat {
        display: flex;
        flex-wrap: wrap;
        gap: 1em 0.5em;
    }

    p {
        text-wrap: balance;
    }

    button.submitting {
        pointer-events: none;
    }

    .spinner {
        display: inline-block;
        width: 1em !important;
        height: 1em !important;
        border: 0.125em solid currentColor;
        border-bottom-color: transparent;
        border-radius: 50%;
        animation: rotation 1s linear infinite;
        transition: border-color 0.4s cubic-bezier(0.25, 1, 0.5, 1);
    }

    @keyframes rotation {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }

    label {
        color: #d3d3d3;
        text-wrap: balance;
    }

    label a {
        color: white;
    }

    button {
        margin-block-start: 2em;
        padding: 1em 2em;
        border: solid 2px;
        border-radius: 4px;
        font-size: 1em;
        color: #4ab9e9;
        background-color: transparent;
        text-shadow: 0 0 6px;
        box-shadow: 0 0 3px 1px #4ab9e9;
        transition: box-shadow 200ms ease-in;
        cursor: pointer;
    }

    button:hover {
        box-shadow: 0 0 9px 2px #4ab9e9;
    }

    iframe {
        width: 100%;
        min-height: 800px;
    }
</style>
