<template>
  <div class="content-div content-div-1">
    <div class="header">
      <h1>{{$t('application_for_new_issue_of_a_liquor_licence')}}</h1>
      <div class="d-flex align-center">
        <BoldLine
          :options="{
            color: this.$vuetify.theme.themes.light.secondary,
            height: 'auto',
            width: '6px',
          }"
          :spacing="'x-stretch'"
        ></BoldLine>
        <h2>{{$t('information_relating_to_the_premises')}}</h2>
      </div>
    </div>
    <div class="body">
      <div class="form-bg-circle hidden-md-and-down">2</div>
      <div class="form-div">
        <v-form v-model="form.valid">
          <h2 class="purple-header em-26">A. {{$t('basic_information')}}</h2>
          <h5 class="mt-8">1 . {{$t('shop_sign')}}</h5>
          <div class="form-section ml-6">
            <v-text-field
              class="tf-half"
              v-model="premises_data.shopSign.chinese"
              :rules="form.fullnameRules"
              label="Chinese"
              outlined
              required
            ></v-text-field>
            <v-text-field
              class="tf-half"
              v-model="premises_data.shopSign.english"
              :rules="form.fullnameRules"
              label="English"
              outlined
              required
            ></v-text-field>
          </div>
          <div class="mt-n1 mb-4 d-flex align-center">
            <h5>2 . Address</h5>
            <v-tooltip right>
              <template v-slot:activator="{ on, attrs }">
                <v-icon
                  class="mb-1 ml-3 mt-3"
                  color="secondary"
                  dark
                  v-bind="attrs"
                  v-on="on"
                >
                  mdi-help-circle
                </v-icon>
              </template>
              <div>
                <div class="d-flex align-center mb-2">
                  <v-icon color="secondary" dark> mdi-help-circle </v-icon>
                  <h3 class="mb-0">Tips:</h3>
                </div>
                <div class="ml-8 c-div">
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed
                  do eiusmod tempor incididunt ut labore et dolore magna aliqua.
                  Ut enim ad minim veniam, quis nostrud exercitation ullamco
                  laboris nisi ut aliquip ex ea commodo consequat.
                </div>
              </div>
            </v-tooltip>
          </div>
          <div class="callout-div detail-box">
            <h5 class="fw-400 em-18 ml-3 mb-3 mt-1">
              If you have a restaurant licence, the address here shall be the
              same as that on the restaurant licence. By entering the restaurant
              licence no. to fill the related information.
            </h5>
            <MultipleTextfield
              class="mt-3 ml-3"
              :inValue="premises_data.restaurant_1_No"
              :refID="restaurant_1_NoMTF.refID"
              :amount="restaurant_1_NoMTF.amount"
              :shouldShow="restaurant_1_NoMTF.error.show"
              :msg="restaurant_1_NoMTF.error.msg"
              :connect="restaurant_1_NoMTF.connect"
              @onInputDone="updateRestaurant_1_NoMTF"
            ></MultipleTextfield>

            <div class="d-flex align-baseline flex-wrap mt-n7 t-wrap">
              <h5 h5 class="fw-400 em-18 ml-3 ma-0 mr-3 mt-6">
                Copy information from restaurant licnece
              </h5>
              <v-btn
                depressed
                class="o-btn-action rounded-pill xs mb-3 mt-3 ml-3"
                color="primary"
                >Copy</v-btn
              >
            </div>
          </div>
          <h5 class="mt-8 ml-6">a. Chinese</h5>
          <div class="form-section ml-6">
            <v-text-field
              class="tf-full mt-2"
              v-model="premises_data.address.chinese[0]"
              :rules="form.addressRules"
              label="室／房／店鋪, 樓數／樓層, 座"
              outlined
              required
            ></v-text-field>
            <v-text-field
              class="tf-full mt-n4"
              v-model="premises_data.address.chinese[1]"
              :rules="form.addressRules"
              label="大廈／村或屋邨名稱, 門牌／地段號碼"
              outlined
              required
            ></v-text-field>
            <v-text-field
              class="tf-full mt-n4"
              v-model="premises_data.address.chinese[2]"
              :rules="form.addressRules"
              label="街道名稱，地區"
              outlined
              required
            ></v-text-field>
            <v-select
              class="mt-n4"
              v-model="premises_data.address.chinese[3]"
              :items="region.tc"
              label="地域"
              outlined
              :menu-props="{offsetY: true}"
            ></v-select>
          </div>
          <h5 class="mt-3 ml-6">b. English</h5>
          <div class="form-section ml-6">
            <v-text-field
              class="tf-full mt-2"
              v-model="premises_data.address.english[0]"
              :rules="form.addressRules"
              label="Room/Flat/Unit, Floor, Block,"
              outlined
              required
            ></v-text-field>
            <v-text-field
              class="tf-full mt-n4"
              v-model="premises_data.address.english[1]"
              :rules="form.addressRules"
              label="Building Name/Name of Estate or Village, Building No./Lot No.,"
              outlined
              required
            ></v-text-field>
            <v-text-field
              class="tf-full mt-n4"
              v-model="premises_data.address.english[2]"
              :rules="form.addressRules"
              label="Street Name, District,"
              outlined
              required
            ></v-text-field>
            <v-select
              class="mt-n4"
              v-model="premises_data.address.english[3]"
              :items="region.en"
              label="Region"
              outlined
              :menu-props="{offsetY: true}"
            ></v-select>
          </div>
          <h5 class="mt-2">3 . Contact</h5>
          <div class="form-section ml-6">
            <v-text-field
              class="tf-half"
              v-model="premises_data.contact.tel"
              :rules="form.fullnameRules"
              label="Tel no."
              outlined
              required
            ></v-text-field>
            <v-text-field
              class="tf-half"
              v-model="premises_data.contact.fax"
              :rules="form.fullnameRules"
              label="Fax no."
              outlined
              required
            ></v-text-field>
          </div>
          <h5 class="mt-2">
            4 . {{$t('size')}}
          </h5>
          <div class="form-section mt-3 justify-start align-baseline ml-6">
            <v-text-field
              class="tf-half mr-4"
              v-model="premises_data.size"
              :rules="form.fullnameRules"
              label="Size"
              outlined
              required
            ></v-text-field>
            <p class="mb-0">m²</p>
          </div>

          <h5 class="mt-3">5 . Premises Details</h5>
          <h5 class="mt-3 mb-5 ml-6 fw-400 em-18">
            a. Business Registration No. of the premises
          </h5>
          <div class="form-section ml-6">
            <MultipleTextfield
              :inValue="premises_data.brNo"
              :refID="premisesBrMTF.refID"
              :amount="premisesBrMTF.amount"
              :shouldShow="premisesBrMTF.error.show"
              :msg="premisesBrMTF.error.msg"
              :connect="premisesBrMTF.connect"
              @onInputDone="updatePremisesBrMTF"
            ></MultipleTextfield>
          </div>
          <div class="mt-1 mb-4 ml-6 d-flex align-center flex-wrap">
            <h5 class="my-0 fw-400 em-18">
              b. If the premises is run by a company
            </h5>
            <v-radio-group v-model="premises_data.q5b" class="ml-6" row>
              <v-radio class="row-radio" :label="'Yes'" :value="true"></v-radio>
              <v-radio
                class="row-radio ml-3"
                :label="'No'"
                :value="false"
              ></v-radio>
            </v-radio-group>
          </div>
          <div v-if="premises_data.q5b == true">
            <h5 class="my-0 fw-400 em-18 ml-10">b (i). Name of company</h5>
            <div class="form-section ml-10 mt-5">
              <v-text-field
                class="tf-half"
                v-model="premises_data.q5b_detail.companyName"
                :rules="form.fullnameRules"
                label="Name"
                outlined
                required
              ></v-text-field>
            </div>
            <h5 class="my-0 fw-400 em-18 ml-10">
              b (ii). Business Registration No. of the company
            </h5>
            <MultipleTextfield
              class="ml-10 mt-5"
              :inValue="premises_data.q5b_detail.companyBr"
              :refID="companyBrMTF.refID"
              :amount="companyBrMTF.amount"
              :shouldShow="companyBrMTF.error.show"
              :msg="companyBrMTF.error.msg"
              :connect="companyBrMTF.connect"
              @onInputDone="updateCompanyBrMTF"
            ></MultipleTextfield>
            <h5 class="my-0 fw-400 em-18 ml-10">
              b (iii). Company No. (if available)
            </h5>
            <MultipleTextfield
              class="ml-10 mt-5"
              :inValue="premises_data.q5b_detail.companyNo"
              :refID="companyNoMTF.refID"
              :amount="companyNoMTF.amount"
              :shouldShow="companyNoMTF.error.show"
              :msg="companyNoMTF.error.msg"
              :connect="companyNoMTF.connect"
              @onInputDone="updateCompanyNoMTF"
            ></MultipleTextfield>
          </div>
          <h2 class="purple-header em-26">
            B. Information Relating to Restaurant Licence
          </h2>
          <div class="d-flex">
            <h5>6.</h5>
            <h5 class="ml-1">
              The type of restaurant licence issued/ being applied for the
              premises under application for liquor licence?
            </h5>
          </div>
          <v-radio-group
            v-model="premises_data.q6_detail"
            class="list-radio-gp mt-4 ml-6 mb-6"
          >
            <v-radio
              class="enhanced"
              :label="'a .  The type pf restaurant licence'"
              :value="'a'"
            ></v-radio>
            <v-radio-group
              v-show="premises_data.q6_detail == 'a'"
              v-model="premises_data.q6a"
              class="list-radio-gp ml-8 my-3"
            >
              <v-radio
                class="mt-5"
                :label="'Light Refreshment Restaurant Licence '"
                :value="'Light'"
              ></v-radio>
              <v-radio
                class="mt-5"
                :label="'General Restaurant Licence'"
                :value="'General'"
              ></v-radio>
              <v-radio
                class="mt-5"
                :label="'Marine Restaurant Licence'"
                :value="'Marine'"
              ></v-radio>
            </v-radio-group>
            <v-radio
              class="enhanced mt-8"
              :label="'b .  The restaurant licence issued/ being applied'"
              :value="'b'"
            ></v-radio>
            <v-radio-group
              v-show="premises_data.q6_detail == 'b'"
              v-model="premises_data.q6b"
              class="list-radio-gp ml-8 my-3"
            >
              <v-radio
                class="mt-5"
                :label="'Issued with Licence'"
                :value="'Issued'"
              ></v-radio>
              <div v-show="premises_data.q6b == 'Issued'">
                <v-radio-group v-model="premises_data.q6b_a" class="ml-10" row>
                  <div class="d-flex">
                    <v-radio
                      class="row-radio mb-0"
                      :label="'Full Licence'"
                      :value="'Full'"
                    ></v-radio>
                    <v-radio
                      class="row-radio ml-3"
                      :label="'Provisional Licence'"
                      :value="'Provisional'"
                    ></v-radio>
                  </div>
                </v-radio-group>
                <h5 class="my-0 fw-400 em-18 ml-10 mt-4">
                  Restaurant Licence Number
                </h5>
                <MultipleTextfield
                  class="ml-10 mt-5"
                  :inValue="premises_data.q6b_a_restaurantNo"
                  :refID="restaurantNoMTF.refID"
                  :amount="restaurantNoMTF.amount"
                  :shouldShow="restaurantNoMTF.error.show"
                  :msg="restaurantNoMTF.error.msg"
                  :connect="restaurantNoMTF.connect"
                  @onInputDone="updateRestaurantNoMTF"
                  :unconnect="true"
                ></MultipleTextfield>
              </div>
              <v-radio
                class="mt-5"
                :label="'Being Applied'"
                :value="'being-applied'"
              ></v-radio>
              <div v-show="premises_data.q6b == 'being-applied'">
                <h5 class="my-0 fw-400 em-18 ml-10 mt-5">
                  File Ref. of Restaurant Licence Application
                </h5>
                <v-text-field
                  class="tf-half ml-10 mt-5"
                  v-model="premises_data.q6b_b_fileRef"
                  :rules="form.fullnameRules"
                  label="File Ref."
                  outlined
                  required
                ></v-text-field>
              </div>
              <v-radio :value="'Not'" class="mt-5">
                <template slot="label">
                  <span
                    >Not under application for or covered by a Restaurant
                    Licence or a Certificate of Compliance issued by the Home
                    Affairs Department <br /><span style="color: #7a7a7a"
                      >(Please complete
                      <span style="color: #4e45d1">Annex I</span> and submit
                      together with the required documents.)</span
                    ></span
                  >
                </template>
              </v-radio>
            </v-radio-group>
          </v-radio-group>
        </v-form>
      </div>
    </div>
    <div v-show="premises_data.q6b == 'Not'" class="body light-purple">
      <div class="form-div">
        <v-form v-model="form.valid">
          <div class="ml-10">
            <h2 class="mt-0 dec">Annex I</h2>
            <h5 class="mt-2 fw-400 em-18">
              For liquor licence application in respect of the premises not
              under application for or covered by a Restaurant Licence or a
              Certificate of Compliance issued by the Home Affairs Department
            </h5>
            <h5 class="mt-2 mt-n2 dec">
              Additional Information to be Provided
            </h5>
            <div class="mt-3 d-flex">
              <h5 class="em-18 mr-2">a.</h5>
              <h5 class="em-18">
                Area of premises for sale or supply of liquor and for
                consumption of liquor on the premises
              </h5>
            </div>
            <div class="form-section mt-3 justify-start align-baseline ml-6">
              <v-text-field
                class="tf-half mr-4"
                v-model="premises_data.an_a_size"
                :rules="form.fullnameRules"
                label="Size"
                outlined
                required
              ></v-text-field>
              <p class="mb-0">m²</p>
            </div>
            <h5 class="em-18">
              b. Installation of Air-conditioning System/Ventilating System:
            </h5>
            <div>
              <v-radio-group v-model="premises_data.an_b.options" class="" row>
                <div class="d-flex">
                  <v-radio
                    class="row-radio mb-0"
                    :label="'Yes'"
                    :value="true"
                  ></v-radio>
                  <v-radio
                    class="row-radio ml-3"
                    :label="'No'"
                    :value="false"
                  ></v-radio>
                </div>
              </v-radio-group>
              <h5 class="em-18 fw-400 mb-4">Type (e.g. water-cooled)</h5>
              <v-text-field
                class="tf-half"
                v-model="premises_data.an_b.type"
                :rules="form.fullnameRules"
                label="Type"
                outlined
                required
              ></v-text-field>
            </div>
            <h5 class="em-18">c. Provision of toilet facilities</h5>
            <v-radio-group
              v-model="premises_data.an_c"
              class="list-radio-gp my-1"
            >
              <v-radio
                class="mt-2"
                :label="'Yes, inside the premises'"
                :value="'Yes_1'"
              ></v-radio>
              <v-radio
                class="mt-5"
                :label="'Yes, public facilities at the building'"
                :value="'Yes_2'"
              ></v-radio>
              <v-radio
                class="mt-5"
                :label="'No, no toilet facilities inside the premises or at the building'"
                :value="'No'"
              ></v-radio>
            </v-radio-group>
            <div class="mt-3 d-flex">
              <h5 class="em-18 mr-2">d.</h5>
              <h5 class="em-18">
                If the premises are under application for or covered by a
                licence or certificate to be issued/issued by government
                departments, please specify
              </h5>
            </div>
            <v-text-field
              class="tf-half"
              v-model="premises_data.an_d"
              :rules="form.fullnameRules"
              label="Licence/Certificate"
              outlined
              required
            ></v-text-field>
            <h5 class="em-18">e. Enclosed</h5>
            <h5 class="em-18">Please enclose the following documents:</h5>
          </div>
        </v-form>
      </div>
      <div class="o-table mb-2">
        <div class="d-flex">
          <h5 class="em-22 mw-6">Additional Information ( Annex l )</h5>
          <h5 class="em-22 mw-4">Last Update</h5>
        </div>
        <BoldLine
          :options="{
            color: 'rgba(177,177,177,0.37)',
            height: '2px',
            width: '100%',
          }"
        ></BoldLine>
        <div class="d-flex py-5">
          <div class="d-flex mw-6 align-center">
            <div class="o-t-item-div">
              A copy of proposed layout plan of the premises
            </div>
            <v-tooltip right>
              <template v-slot:activator="{ on, attrs }">
                <v-icon
                  class="ml-2"
                  color="secondary"
                  dark
                  v-bind="attrs"
                  v-on="on"
                >
                  mdi-help-circle
                </v-icon>
              </template>
              <div>
                <div class="d-flex align-center mb-2">
                  <v-icon color="secondary" dark> mdi-help-circle </v-icon>
                  <h3 class="mb-0">Tips:</h3>
                </div>
                <div class="ml-8 c-div">
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed
                  do eiusmod tempor incididunt ut labore et dolore magna aliqua.
                  Ut enim ad minim veniam, quis nostrud exercitation ullamco
                  laboris nisi ut aliquip ex ea commodo consequat.
                </div>
              </div>
            </v-tooltip>
          </div>
          <div class="d-flex align-center justify-space-between mw-4">
            <h5 class="ma-0 ml-1 em-18 fw-400">-</h5>
            <v-btn
              depressed
              :disabled="btnDisabled"
              class="o-btn-action small mr-1 mt-0"
              style="justify-self: flex-start"
              color="primary"
              >Choose file</v-btn
            >
          </div>
        </div>
        <div class="d-flex py-5">
          <div class="d-flex mw-6 align-center">
            <div class="o-t-item-div">
              A copy of proposed ventilating system layout plan of the premises
              with their Supplier Certificate
            </div>
            <v-tooltip right>
              <template v-slot:activator="{ on, attrs }">
                <v-icon
                  class=""
                  color="secondary"
                  dark
                  v-bind="attrs"
                  v-on="on"
                >
                  mdi-help-circle
                </v-icon>
              </template>
              <div>
                <div class="d-flex align-center mb-2">
                  <v-icon color="secondary" dark> mdi-help-circle </v-icon>
                  <h3 class="mb-0">Tips:</h3>
                </div>
                <div class="ml-8 c-div">
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed
                  do eiusmod tempor incididunt ut labore et dolore magna aliqua.
                  Ut enim ad minim veniam, quis nostrud exercitation ullamco
                  laboris nisi ut aliquip ex ea commodo consequat.
                </div>
              </div>
            </v-tooltip>
          </div>
          <div class="d-flex align-center justify-space-between mw-4">
            <h5 class="ma-0 ml-1 em-18 fw-400">-</h5>
            <v-btn
              depressed
              :disabled="btnDisabled"
              class="o-btn-action small mr-1 mt-0"
              style="justify-self: flex-start"
              color="primary"
              >Choose file</v-btn
            >
          </div>
        </div>
        <div class="d-flex py-5">
          <div class="d-flex mw-6 align-center">
            <div class="o-t-item-div">
              A copy of of location plan of the premises
            </div>
            <v-tooltip right>
              <template v-slot:activator="{ on, attrs }">
                <v-icon
                  class="ml-2"
                  color="secondary"
                  dark
                  v-bind="attrs"
                  v-on="on"
                >
                  mdi-help-circle
                </v-icon>
              </template>
              <div>
                <div class="d-flex align-center mb-2">
                  <v-icon color="secondary" dark> mdi-help-circle </v-icon>
                  <h3 class="mb-0">Tips:</h3>
                </div>
                <div class="ml-8 c-div">
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed
                  do eiusmod tempor incididunt ut labore et dolore magna aliqua.
                  Ut enim ad minim veniam, quis nostrud exercitation ullamco
                  laboris nisi ut aliquip ex ea commodo consequat.
                </div>
              </div>
            </v-tooltip>
          </div>
          <div class="d-flex align-center justify-space-between mw-4">
            <h5 class="ma-0 ml-1 em-18 fw-400">-</h5>
            <v-btn
              depressed
              :disabled="btnDisabled"
              class="o-btn-action small mr-1 mt-0"
              style="justify-self: flex-start"
              color="primary"
              >Choose file</v-btn
            >
          </div>
        </div>
      </div>
      <div class="form-div">
        <p class="em-16">
          Whenever there are changes to the submitted plans for the application,
          the applicant is required to highlight any proposed changes on the
          revised plans with colour pens and simple descriptions before making
          submission to the Liquor Licensing Board for consideration and
          referral to other government departments for processing. Revised plans
          not in compliance with this requirement will be rejected. Applicant
          should note that the Liquor Licensing Board and other government
          departments concerned would not be responsible for any delay caused by
          the errors and omissions in highlighting all changes on the plans.
        </p>
        <div class="text-box">
          <h3>Notes for enclosure of Annex I</h3>
          <ol class="ml-0">
            <li>
              <p class="em-16 mt-4">
                Annex l must be accompanied by the liquor licence application
                form and the following plans; otherwise the Department is unable
                to process the application:
              </p>
              <ol type="a" class="ml-0">
                <li>
                  <p class="em-16 mt-4">
                    5 identical copies of proposed layout plans1 are required to
                    show the layout of the premises including the portion for
                    sale of supply of liquor and for consumption of liquor on
                    the premises. Such plans should be drawn to scale (of not
                    less than 1:100) in metric unit.
                  </p>
                </li>
                <li>
                  <p class="em-16 mt-4">
                    3 identical copies of proposed ventilating system2 layout
                    plans together with the Supplier Certificate are required if
                    the ventilating system is installed in the premises. Such
                    plans should be drawn to scale (of not less than 1:100) in
                    metric unit.
                  </p>
                </li>
                <li>
                  <p class="em-16 mt-4">
                    3 identical copies of location maps drawn to scale of
                    1:1000, in metric unit, are required to clearly indicate the
                    location of the premises
                  </p>
                </li>
              </ol>
            </li>
            <li>
              <p class="em-16 mt-4">
                The application will be referred to the Hong Kong Police Force,
                District Office of the Home Affairs Department, Planning
                Department, Fire Services Department, Buildings
                Department/Housing Department/Architectural Services Department
                etc. and government departments concerned for comment. It will
                take longer processing time than normal liquor licence
                applications.
              </p>
            </li>
            <li>
              <p class="em-16 mt-4">
                Except for premises in government properties or the Housing
                Authority’s properties, certification made by recognised
                professional(s) (i.e. authorised persons/structural engineers
                registered under Section 3 of the Buildings Ordinance (Cap.
                123)) certifying that the premises are free of unauthorised
                building works shall be submitted (in person or by mail) to the
                Liquor Licensing Board in prescribed form (FEHB 267) in
                accordance with the corresponding guidelines, where appropriate,
                listed as follows:
              </p>
              <ol type="a" class="ml-0">
                <li>
                  <p class="em-16 mt-4">
                    “Certification of Food Business Premises Free of
                    Unauthorised Building Works – Guidelines for Authorised
                    Persons and Registered Structural Engineers” issued by the
                    Director of Buildings
                  </p>
                </li>
                <li>
                  <p class="em-16 mt-4">
                    “Certification of Food Business Premises Free of
                    Unauthorised Building Works – Guidelines for Authorised
                    Persons and Registered Structural Engineers” (applicable to
                    the properties divested to Link Asset Management Limited)
                    issued by the Independent Checking Unit of the Housing
                    Department
                  </p>
                </li>
              </ol>
            </li>
            <li>
              <p class="em-16 mt-4">
                If a ventilating system is installed, the standard of
                ventilation shall be a supply of not less than 17 cubic meters
                of outside air per hour for each person accommodated on the
                premises.
              </p>
            </li>
            <li>
              <p class="em-16 mt-4">
                Whenever there are changes to the submitted plans for the
                application, the applicant is required to highlight any proposed
                changes on the revised plans with colour pens and simple
                descriptions before making submission to the Liquor Licensing
                Board for consideration and referral to other government
                departments for processing. Revised plans not in compliance with
                this requirement will be rejected. Applicant should note that
                the Liquor Licensing Board and other government departments
                concerned would not be responsible for any delay caused by the
                errors and omissions in highlighting all changes on the plans.
              </p>
            </li>
          </ol>
        </div>
      </div>
    </div>
    <div class="body">
      <div class="form-div">
        <v-form v-model="form.valid">
          <h2 class="purple-header em-26">
            C. Information Relating to The Building
          </h2>
          <h5 class="mt-8">
            7 . What is the approved use of the building in which the premises
            are located?
          </h5>
          <v-radio-group
            v-model="premises_data.q7.options"
            class="list-radio-gp ml-8"
          >
            <v-radio
              class="mt-2"
              :label="'Mixed Residential and Commercial Uses'"
              :value="'Mixed'"
            ></v-radio>
            <v-radio
              class="mt-5"
              :label="'Wholly Commercial Use'"
              :value="'Commercial'"
            ></v-radio>
            <v-radio
              class="mt-5"
              :label="'Other use, please give details'"
              :value="'Other'"
            ></v-radio>
          </v-radio-group>
          <v-text-field
            class="tf-half ml-15 mt-5"
            v-model="premises_data.q7.others"
            :rules="form.fullnameRules"
            label="File Ref."
            outlined
            required
          ></v-text-field>
          <h5 class="mt-6">8 . The premises have</h5>
          <v-radio-group
            v-model="premises_data.q8"
            class="list-radio-gp ml-8 my-3 mb-6"
          >
            <v-radio
              class="mt-2"
              :label="'Independent access'"
              :value="'Independent'"
            ></v-radio>
            <v-radio
              class="mt-5"
              :label="'Shared access with the other portion of the building'"
              :value="'Shared'"
            ></v-radio>
          </v-radio-group>
        </v-form>
      </div>
    </div>
    <div class="footer mt-6">
      <v-btn class="footer-btn b-dark">{{$t('save_draft')}}</v-btn>
      <v-btn
        class="footer-btn b-primary"
        :disabled="false"
        @click="$router.push({ name: 'NewInfoApplicant' })"
        >{{$t('save_and_next')}}</v-btn
      >
    </div>
  </div>
</template>

<script>
import BoldLine from "../../components/misc/bold-line";
import MultipleTextfield from "../../components/misc/multiple-textfield";
// @ is an alias to /src

export default {
  name: "NewIP",
  components: {
    BoldLine,
    MultipleTextfield,
  },
  data: function () {
    return {
      agree: false,
      btnDisabled: false,
      form: {
        valid: false,
        fullnameRules: [(v) => !!v || "Name is required"],
        emailRules: [
          (v) => !!v || "Email is required",
          (v) => /.+@.+/.test(v) || "Email must be valid",
        ],
      },
      premises_data: {
        address: {
          chinese: ["", "", "", ""],
          english: ["", "", "", ""],
        },
        restaurant_1_No: "".split(""),
        contact: {
          tel: "",
          fax: "",
        },
        shopSign: {
          chinese: "",
          english: "",
        },
        brNo: "".split(""),
        size: "",
        q5b: undefined,
        q5b_detail: {
          companyName: "",
          companyBr: "".split(""),
          companyNo: "".split(""),
        },
        q6_detail: "",
        q6a: "",
        q6b: "",
        q6b_a: "",
        q6b_a_restaurantNo: "".split(""),
        q6b_b_fileRef: "",
        q7: {
          options: "",
          others: "",
        },
        q8: "",
        an_a_size: "",
        an_b: { options: "", type: "" },
        an_c: "",
        an_d: "",
      },
      region: {
        tc: ["香港", "九龍", "新界"],
        en: ["Hong Kong", "Kowloon", "New Territories"],
      },
      premisesBrMTF: {
        value: "",
        refID: "premisesBr",
        error: { show: false, msg: "Invalid input" },
        amount: 11,
        connect: [7],
      },
      companyBrMTF: {
        value: "",
        refID: "companyBr",
        error: { show: false, msg: "Invalid input" },
        amount: 11,
        connect: [7],
      },
      companyNoMTF: {
        value: "",
        refID: "companNo",
        error: { show: false, msg: "Invalid input" },
        amount: 7,
        connect: [],
      },
      restaurant_1_NoMTF: {
        value: "",
        refID: "restaurant_1_No",
        error: { show: false, msg: "Invalid input" },
        amount: 10,
        connect: [1, 3],
      },
      restaurantNoMTF: {
        value: "",
        refID: "restaurantNo",
        error: { show: false, msg: "Invalid input" },
        amount: 10,
        connect: [1, 3],
      },
    };
  },
  methods: {
    updatePremisesBrMTF: function (inValue, i) {
      this.updateMTF(inValue, i, this.premisesBrMTF);
    },
    updateCompanyBrMTF: function (inValue, i) {
      this.updateMTF(inValue, i, this.companyBrMTF);
    },
    updateCompanyNoMTF: function (inValue, i) {
      this.updateMTF(inValue, i, this.companyNoMTF);
    },
    updateRestaurantNoMTF: function (inValue, i) {
      this.updateMTF(inValue, i, this.restaurantNoMTF);
    },
    updateRestaurant_1_NoMTF: function (inValue, i) {
      this.updateMTF(inValue, i, this.restaurant_1_NoMTF);
    },
    updateMTF: function (inValue, i, target) {
      var str = this.joinStringWithMTF(inValue, target.connect);
      target.value = str;
      const lastindex = target.amount - 1;
      if (i == lastindex) {
        if (str.length < target.amount + target.connect.length) {
          target.error.show = true;
        } else {
          target.error.show = false;
        }
      }
    },
    joinStringWithMTF: function (inValue, connect) {
      const temp = [];
      inValue.forEach((element, i) => {
        if (element != null && element != "") {
          temp[temp.length] = element;
        }
      });
      if (connect.length > 0) {
        var n = 1;
        connect.forEach((i) => {
          if (temp.length > i + n) {
            console.log(temp.length);
            temp.splice(i + n, 0, "-");
            n++;
          }
        });
      }
      const str = temp.join("");
      return str;
    },
  },
  activated() {
    this.$emit("updateCurrent", 2);
    this.dialog = true;
  },
};
</script>

<style scoped lang="scss">
.main-container {
  width: 100%;
  height: 100%;
  flex-direction: row;
  align-items: flex-start;
}

h2.dec {
  font-size: 1.5625em;
  text-decoration: underline;
}

.form-div {
  width: clamp(280px, 100%, 720px);
  .o-btn-action {
    margin-top: 32.5px;
  }
}

h5 {
  color: black;
}

p.em-16 {
  font-size: 1em;
  line-height: 1.2em;
  color: $ols-t-darkGrey;
}

h5.dec {
  font-size: 1.25em;
  text-decoration: underline;
}

h5.fw-400 {
  color: $ols-t-dark;
  margin-top: 13px;
  margin-bottom: 40px;
}

h5.em-18 {
  font-size: 1.125em;
}

h2.em-26 {
  font-size: 1.5625em;
}

.big-gap {
  margin-right: 16px;
}

//md and down
@media screen and (max-width: 1263px) {
  .main-container {
    width: 100%;
    height: 100%;
    flex-direction: column;
  }

  h5.em-18 {
    font-size: 1em;
  }

  p.em-16 {
    font-size: 0.9375em;
    line-height: 1.1em;
  }

  h5.dec {
    font-size: 1.175em;
    text-decoration: underline;
  }

  h2.em-26 {
    font-size: 1.4em;
  }

  h2.dec {
    font-size: 1.375em;
    text-decoration: underline;
  }

  .big-gap {
    margin-right: 8px;
  }
}
</style>
