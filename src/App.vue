<template>
  <v-app>
    <v-app-bar app class="hidden-sm-and-down navigation">
      <div class="d-flex align-center">
        <a href="https://brightid.org">
          <v-img
            alt="Vuetify Logo"
            class="shrink mr-2"
            contain
            src="https://miro.medium.com/max/1200/1*FteDjn3xH6NEQj6lTw1tow.png"
            transition="scale-transition"
            width="150"
          />
        </a>
      </div>
      <v-spacer></v-spacer>
      <div class="hidden-sm-and-down">
        

        <a href="https://medium.com/brightid" class="mx-6 black--text">Blog</a>
        <a
          href="https://www.bonfire.com/store/brightid-swag/"
          class="mx-6 black--text"
          >Store</a
        >
      </div>

      <v-btn
        color="black"
        class="hidden-sm-and-down"
        href="https://discord.gg/WehNg4B4f4"
        target="_blank"
        outlined
        rounded
      >
        <span class="mr-2">Contact Us</span>
      </v-btn>
    </v-app-bar>
    <v-app-bar app dark color="black darken-3" class="hidden-md-and-up">
      <v-toolbar-title
        ><a href="https://brightid.org">
          <v-img
            alt="Vuetify Logo"
            class="shrink mr-2"
            contain
            src="https://uploads-ssl.webflow.com/5e54622b3f6e65be8baf0653/5e57958e0eb38846a2658298_brightid-reversed.svg"
            transition="scale-transition"
            width="150"
          /> </a
      ></v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon @click.native="dialog = true">
        <v-icon color="white">mdi-menu</v-icon>
      </v-btn>
      <v-dialog
        v-model="dialog"
        fullscreen
        hide-overlay
        transition="dialog-bottom-transition"
      >
        <v-card class="black">
          <v-toolbar flat color="black darken-2">
            <v-toolbar-title class="white--text"
              ><a href="https://brightid.org">
                <v-img
                  alt="Vuetify Logo"
                  class="shrink mr-2"
                  contain
                  src="https://uploads-ssl.webflow.com/5e54622b3f6e65be8baf0653/5e57958e0eb38846a2658298_brightid-reversed.svg"
                  transition="scale-transition"
                  width="150"
                /> </a
            ></v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn icon @click.native="dialog = false">
              <v-icon class="white--text">mdi-close</v-icon>
            </v-btn>
          </v-toolbar>

          <v-list class="black">
            <v-row justify="center" class="black py-4">
              <a href="https://medium.com/brightid" class="text-h5">Blog</a>
            </v-row>
            <v-row justify="center" class="black py-4">
              <a
                href="https://www.bonfire.com/store/brightid-swag/"
                class="text-h5"
                >Store</a
              >
            </v-row>
            <v-row justify="center" class="black py-4">
              <a href="https://discord.gg/WehNg4B4f4" class="text-h5"
                >Contact Us</a
              >
            </v-row>
          </v-list>
        </v-card>
      </v-dialog>
    </v-app-bar>

    <v-main class="pt-md-15 pt-0">
      <v-row class="header">
        <v-col align-self="center" cols="5" offset="1"
          ><h1 class="text-md-h3 text-h5 font-weight-bold">
            BrightID <br />
            Connection Parties
          </h1></v-col
        >
        <v-col cols="5" align-self="center">
          <v-img src="./assets/Group 25.png" contain height="300"></v-img>
        </v-col>
      </v-row>

      <v-container>
        <v-row class="mt-5">
          <v-col offset-md="1">
            <h2 class="text-md-h6 text-subtitle-1 font-weight-bold changefont">
              Find the best schedule for you
            </h2>
          </v-col>
        </v-row>
        <v-row>
          <v-col offset-md="1" cols="3" md="2" align-self="center">
            <span>Times are in</span>
          </v-col>
          <v-col align-self="center" cols="8" md="4">
            <v-autocomplete
              color="red--text"
              v-model="timeZoneSelect"
              :items="listTimeZone"
              label="select timezone"
            ></v-autocomplete>
            <p class="text-caption">Current time: {{ clock }}</p>
          </v-col>
          <v-col
            offset-md="1"
            cols="4"
            align-self="center"
            class="blue--text d-none d-md-block"
          >
            <i @click="pervWeek" class="hand_icon mx-2"
              ><v-icon class="blue--text">mdi-chevron-left</v-icon></i
            >
            <span>{{ weekPeriodString }}</span>
            <i @click="nextWeek" class="hand_icon blue--text mx-2"
              ><v-icon class="blue--text">mdi-chevron-right</v-icon></i
            >
          </v-col>
        </v-row>
        <v-row class="mt-10 d-none d-md-block">
          <v-col md="12">
            <v-row class="seven-col">
              <v-col cols="1"></v-col>
              <v-col
                class="text-center day-week"
                :class="{
                  last_days: dayOfWeek > 0 && !showThisWeek,
                  today: dayOfWeek === 0 && !showThisWeek,
                }"
                cols="1"
              >
                <h5 class="text-h5 font-weight-bold">Mon</h5>
                <b>{{ weekDate[0] }}</b>
                <h5 class="today_lable" v-if="dayOfWeek === 0 && !showThisWeek">
                  Today
                </h5>
              </v-col>
              <v-col
                class="text-center day-week"
                :class="{
                  last_days: dayOfWeek > 1 && !showThisWeek,
                  today: dayOfWeek === 1 && !showThisWeek,
                }"
                cols="1"
              >
                <h5 class="text-h5 font-weight-bold">Tue</h5>
                <b>{{ weekDate[1] }}</b>
                <h5 class="today_lable" v-if="dayOfWeek === 1 && !showThisWeek">
                  Today
                </h5>
              </v-col>
              <v-col
                class="text-center day-week"
                :class="{
                  last_days: dayOfWeek > 2 && !showThisWeek,
                  today: dayOfWeek === 2 && !showThisWeek,
                }"
                cols="1"
              >
                <h5 class="text-h5 font-weight-bold">Wed</h5>
                <b>{{ weekDate[2] }}</b>
                <h5 class="today_lable" v-if="dayOfWeek === 2 && !showThisWeek">
                  Today
                </h5>
              </v-col>
              <v-col
                class="text-center day-week"
                :class="{
                  last_days: dayOfWeek > 3 && !showThisWeek,
                  today: dayOfWeek === 3 && !showThisWeek,
                }"
                cols="1"
              >
                <h5 class="text-h5 font-weight-bold">Thu</h5>
                <b>{{ weekDate[3] }}</b>
                <h5 class="today_lable" v-if="dayOfWeek === 3 && !showThisWeek">
                  Today
                </h5>
              </v-col>
              <v-col
                class="text-center day-week"
                :class="{
                  last_days: dayOfWeek > 4 && !showThisWeek,
                  today: dayOfWeek === 4 && !showThisWeek,
                }"
                cols="1"
              >
                <h5 class="text-h5 font-weight-bold">Fri</h5>
                <b>{{ weekDate[4] }}</b>
                <h5 class="today_lable" v-if="dayOfWeek === 4 && !showThisWeek">
                  Today
                </h5>
              </v-col>
              <v-col
                class="text-center day-week"
                :class="{
                  last_days: dayOfWeek > 5 && !showThisWeek,
                  today: dayOfWeek === 5 && !showThisWeek,
                }"
                cols="1"
              >
                <h5 class="text-h5 font-weight-bold">Sat</h5>
                <b>{{ weekDate[5] }}</b>
                <h5 class="today_lable" v-if="dayOfWeek === 5 && !showThisWeek">
                  Today
                </h5>
              </v-col>
              <v-col
                class="text-center day-week"
                :class="{
                  last_days: dayOfWeek > 6 && !showThisWeek,
                  today: dayOfWeek === 6 && !showThisWeek,
                }"
                cols="1"
              >
                <h5 class="text-h5 font-weight-bold">Sun</h5>
                <b>{{ weekDate[6] }}</b>
                <h5 class="today_lable" v-if="dayOfWeek === 6 && !showThisWeek">
                  Today
                </h5>
              </v-col>
            </v-row>
          </v-col>
        </v-row>

        <v-row class="d-none d-md-block">
          <v-col cols="12">
            <v-row
              class="seven-col"
              v-for="(meetindex, i) in meetingtimelist"
              :key="i"
            >
              <v-col cols="1" align-self="center" class="pr-10">
                <span class="text-h6 font-weight-black">{{ i }}</span>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="meetindex.Mon != undefined"
                  :title="meetindex.Mon.title"
                  :app="meetindex.Mon.app"
                  :link="meetindex.Mon.link"
                  :dayStatus="dayStatus(0, i)"
                  :time="i"
                  :date="weekDate[0]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="meetindex.Tue != undefined"
                  :title="meetindex.Tue.title"
                  :app="meetindex.Tue.app"
                  :link="meetindex.Tue.link"
                  :dayStatus="dayStatus(1, i)"
                  :time="i"
                  :date="weekDate[1]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="meetindex.Wed != undefined"
                  :title="meetindex.Wed.title"
                  :app="meetindex.Wed.app"
                  :link="meetindex.Wed.link"
                  :dayStatus="dayStatus(2, i)"
                  :time="i"
                  :date="weekDate[2]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="meetindex.Thu != undefined"
                  :title="meetindex.Thu.title"
                  :app="meetindex.Thu.app"
                  :link="meetindex.Thu.link"
                  :dayStatus="dayStatus(3, i)"
                  :time="i"
                  :date="weekDate[3]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="meetindex.Fri != undefined"
                  :title="meetindex.Fri.title"
                  :app="meetindex.Fri.app"
                  :link="meetindex.Fri.link"
                  :dayStatus="dayStatus(4, i)"
                  :time="i"
                  :date="weekDate[4]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="meetindex.Sat != undefined"
                  :title="meetindex.Sat.title"
                  :app="meetindex.Sat.app"
                  :link="meetindex.Sat.link"
                  :dayStatus="dayStatus(5, i)"
                  :time="i"
                  :date="weekDate[5]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="meetindex.Sun != undefined"
                  :title="meetindex.Sun.title"
                  :app="meetindex.Sun.app"
                  :link="meetindex.Sun.link"
                  :dayStatus="dayStatus(6, i)"
                  :time="i"
                  :date="weekDate[6]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
            </v-row>
            <v-row
              class="seven-col"
              v-for="(meetindex, i) in meetingSpecial"
              :key="i"
            >
              <v-col cols="1" align-self="center" class="pr-10">
                <span
                  v-if="
                    specialToday(meetindex.Mon, weekDate[0]) ||
                    specialToday(meetindex.Tue, weekDate[1]) ||
                    specialToday(meetindex.Wed, weekDate[2]) ||
                    specialToday(meetindex.Thu, weekDate[3]) ||
                    specialToday(meetindex.Fri, weekDate[4]) ||
                    specialToday(meetindex.Sat, weekDate[5]) ||
                    specialToday(meetindex.Sun, weekDate[6])
                  "
                  class="text-h6 font-weight-black"
                  >{{ i }}</span
                >
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="specialToday(meetindex.Mon, weekDate[0])"
                  :title="meetindex.Mon.title"
                  :app="meetindex.Mon.app"
                  :link="meetindex.Mon.link"
                  :dayStatus="dayStatus(0, i)"
                  :time="i"
                  :date="weekDate[0]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="specialToday(meetindex.Tue, weekDate[1])"
                  :title="meetindex.Tue.title"
                  :app="meetindex.Tue.app"
                  :link="meetindex.Tue.link"
                  :dayStatus="dayStatus(1, i)"
                  :time="i"
                  :date="weekDate[1]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="specialToday(meetindex.Wed, weekDate[2])"
                  :title="meetindex.Wed.title"
                  :app="meetindex.Wed.app"
                  :link="meetindex.Wed.link"
                  :dayStatus="dayStatus(2, i)"
                  :time="i"
                  :date="weekDate[2]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="specialToday(meetindex.Thu, weekDate[3])"
                  :title="meetindex.Thu.title"
                  :app="meetindex.Thu.app"
                  :link="meetindex.Thu.link"
                  :dayStatus="dayStatus(3, i)"
                  :time="i"
                  :date="weekDate[3]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="specialToday(meetindex.Fri, weekDate[4])"
                  :title="meetindex.Fri.title"
                  :app="meetindex.Fri.app"
                  :link="meetindex.Fri.link"
                  :dayStatus="dayStatus(4, i)"
                  :time="i"
                  :date="weekDate[4]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="specialToday(meetindex.Sat, weekDate[5])"
                  :title="meetindex.Sat.title"
                  :app="meetindex.Sat.app"
                  :link="meetindex.Sat.link"
                  :dayStatus="dayStatus(5, i)"
                  :time="i"
                  :date="weekDate[5]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
              <v-col cols="1">
                <MeetingCard
                  v-if="specialToday(meetindex.Sun, weekDate[6])"
                  :title="meetindex.Sun.title"
                  :app="meetindex.Sun.app"
                  :link="meetindex.Sun.link"
                  :dayStatus="dayStatus(6, i)"
                  :time="i"
                  :date="weekDate[6]"
                  :year="weekPeriodString"
                  :timeZone="timeZoneSelect"
                ></MeetingCard>
              </v-col>
            </v-row>
          </v-col>
        </v-row>
        <v-row class="d-md-none mb-4">
          <v-col class="pl-0" offset="2" cols="1" align-self="center">
            <v-icon @click="previousMobileDay" class="text-h4 blue--text"
              >mdi-chevron-left</v-icon
            >
          </v-col>
          <v-col
            class="text-center day-week"
            :class="{
              last_days: dayOfWeek > mobileDay,
              today: dayOfWeek === mobileDay,
            }"
            cols="4"
          >
            <h5 class="subtitle-1 font-weight-bold">
              {{ dataNumToMonth[mobileDay] }}
            </h5>
            <b class="subtitle-2">{{ weekDate[mobileDay] }}</b>
            <h5 class="today_lable" v-if="dayOfWeek === mobileDay">Today</h5>
          </v-col>
          <v-col
            v-if="mobileDay < 6"
            class="text-center day-week"
            :class="{
              last_days: dayOfWeek > mobileDay + 1,
              today: dayOfWeek === mobileDay + 1,
            }"
            cols="4"
          >
            <h5 class="subtitle-1 font-weight-bold">
              {{ dataNumToMonth[mobileDay + 1] }}
            </h5>
            <b class="subtitle-2">{{ weekDate[mobileDay + 1] }}</b>
            <h5 class="today_lable" v-if="dayOfWeek === mobileDay + 1">
              Today
            </h5>
          </v-col>
          <v-col align-self="center" cols="1" class="pl-0 text-left">
            <i>
              <v-icon
                @click="nextMobileDay"
                class="text-h4 blue--text text-left"
                >mdi-chevron-right</v-icon
              >
            </i>
          </v-col>
        </v-row>
        <v-row
          class="seven-col d-md-none"
          v-for="(meetindex, i) in meetingtimelist"
          :key="i"
        >
          <v-col cols="2" align-self="center">
            <span class="text-caption font-weight-black">{{ i }}</span>
          </v-col>
          <v-col cols="4" offset="1" class="px-1">
            <MeetingCard
              v-if="meetindex[dataNumToMonth[mobileDay]] != undefined"
              :title="meetindex[dataNumToMonth[mobileDay]].title"
              :app="meetindex[dataNumToMonth[mobileDay]].app"
              :link="meetindex[dataNumToMonth[mobileDay]].link"
              :dayStatus="dayStatus(mobileDay, i)"
              :time="i"
              :date="weekDate[mobileDay]"
              :year="weekPeriodString"
              :timeZone="timeZoneSelect"
            ></MeetingCard>
          </v-col>
          <v-col cols="4" class="px-1">
            <MeetingCard
              v-if="meetindex[dataNumToMonth[mobileDay + 1]] != undefined"
              :title="meetindex[dataNumToMonth[mobileDay + 1]].title"
              :app="meetindex[dataNumToMonth[mobileDay + 1]].app"
              :link="meetindex[dataNumToMonth[mobileDay + 1]].link"
              :dayStatus="dayStatus(mobileDay + 1, i)"
              :time="i"
              :date="weekDate[mobileDay + 1]"
              :year="weekPeriodString"
              :timeZone="timeZoneSelect"
            ></MeetingCard>
          </v-col>
        </v-row>
        <v-row
          class="seven-col d-md-none"
          v-for="(meetindex, i) in meetingSpecial"
          :key="i"
        >
          <v-col cols="2" align-self="center">
            <span
              v-if="
                specialToday(
                  meetindex[dataNumToMonth[mobileDay]],
                  weekDate[mobileDay]
                ) ||
                specialToday(
                  meetindex[dataNumToMonth[mobileDay + 1]],
                  weekDate[mobileDay + 1]
                )
              "
              class="text-caption font-weight-black"
              >{{ i }}</span
            >
          </v-col>
          <v-col cols="4" offset="1" class="px-1">
            <MeetingCard
              v-if="
                meetindex[dataNumToMonth[mobileDay]] != undefined &&
                specialToday(
                  meetindex[dataNumToMonth[mobileDay]],
                  weekDate[mobileDay]
                )
              "
              :title="meetindex[dataNumToMonth[mobileDay]].title"
              :app="meetindex[dataNumToMonth[mobileDay]].app"
              :link="meetindex[dataNumToMonth[mobileDay]].link"
              :dayStatus="dayStatus(mobileDay, i)"
              :time="i"
              :date="weekDate[mobileDay]"
              :year="weekPeriodString"
              :timeZone="timeZoneSelect"
            ></MeetingCard>
          </v-col>
          <v-col cols="4" class="px-1">
            <MeetingCard
              v-if="
                meetindex[dataNumToMonth[mobileDay + 1]] != undefined &&
                specialToday(
                  meetindex[dataNumToMonth[mobileDay + 1]],
                  weekDate[mobileDay + 1]
                )
              "
              :title="meetindex[dataNumToMonth[mobileDay + 1]].title"
              :app="meetindex[dataNumToMonth[mobileDay + 1]].app"
              :link="meetindex[dataNumToMonth[mobileDay + 1]].link"
              :dayStatus="dayStatus(mobileDay + 1, i)"
              :time="i"
              :date="weekDate[mobileDay + 1]"
              :year="weekPeriodString"
              :timeZone="timeZoneSelect"
            ></MeetingCard>
          </v-col>
        </v-row>
      </v-container>
      <v-footer height="150px" color="secondary" class="px-10 footerstyle">
        <h5 class="text-caption-1 mr-1">COPYRIGHT ©</h5>
        <a
          class="text-caption-1 black--text"
          href="https://github.com/BrightID/BrightID-Constitution"
          >BrightID Main LLC</a
        >
        <v-spacer></v-spacer>
        <h5 class="text-h5 black--text">Join the BrightID community</h5>

        <a href="https://twitter.com/BrightIDProject" class="ml-2">
          <v-icon dark>mdi-twitter</v-icon>
        </a>
        <a href="https://medium.com/brightid">
          <v-icon dark>mdi-alpha-m-box</v-icon>
        </a>
        <a href="https://t.me/brightidofficial">
          <v-icon dark>mdi-telegram</v-icon>
        </a>
        <a href="https://discord.gg/WehNg4B4f4" class="mr-2">
          <v-icon dark>mdi-discord</v-icon>
        </a>
        <v-spacer></v-spacer>
        <a href="https://www.brightid.org/whitepaper">Privacy Policy</a>
        <span class="mx-2">|</span>
        <a href="https://www.brightid.org/whitepaper">Whitepaper</a>
      </v-footer>
    </v-main>
  </v-app>
</template>
 
<script>
import MeetingCard from "./components/MeetingCard";
import moment from "moment-timezone";
import axios from "axios";

function dayNumber(day) {
  if (day === "Mon") return 1;
  if (day === "Tue") return 2;
  if (day === "Wed") return 3;
  if (day === "Thu") return 4;
  if (day === "Fri") return 5;
  if (day === "Sat") return 6;
  if (day === "Sun") return 0;
}
var numToDay = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
var mobileNumToDay = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];
var numToMonth = [
  "Jan",
  "Feb",
  "Mar",
  "Apr",
  "May",
  "June",
  "July",
  "Aug",
  "Sept",
  "Oct",
  "Nov",
  "Dec",
];
function sevenDayOfMonth(firstDay, firstDayMonth, firstDayYear) {
  var date = new Date(firstDayMonth + " " + firstDay + " " + firstDayYear);
  var arr = [];
  for (var i = 0; i < 12; i++) {
    arr[i] = numToMonth[date.getMonth()] + " " + date.getDate();
    date.setDate(date.getDate() + 1);
  }
  return arr;
}
function objectificationSpecialTime(json, timezone) {
  var meets = [];
  for (const meet in json) {
    let temp = new Object();
    temp.day =
      numToDay[
        new Date(json[meet].year, json[meet].month, json[meet].date).getDay()
      ];
    temp.numDay = dayNumber(temp.day);
    temp.startTime = json[meet].time.split(" - ")[0];
    temp.endTime = json[meet].time.split(" - ")[1];
    temp.app = json[meet].app;
    temp.title = json[meet].title;
    temp.link = json[meet].link;
    temp = convertToLocal(
      temp,
      timezone,
      json[meet].year,
      json[meet].month,
      json[meet].date
    );

    if (typeof meets[temp.startTime + "- " + temp.endTime] === "undefined") {
      let dayObject = {};
      dayObject.title = temp.title;
      dayObject.app = temp.app;
      dayObject.link = temp.link;
      dayObject.date = json[meet].date;
      dayObject.month = json[meet].month;
      dayObject.year = json[meet].year;

      meets[temp.startTime + "- " + temp.endTime] = {};
      meets[temp.startTime + "- " + temp.endTime][temp.day] = dayObject;
    } else {
      let dayObject = {};
      dayObject.title = temp.title;
      dayObject.app = temp.app;
      dayObject.link = temp.link;
      dayObject.date = json[meet].date;
      dayObject.month = json[meet].month;
      dayObject.year = json[meet].year;
      meets[temp.startTime + "- " + temp.endTime][temp.day] = dayObject;
    }
  }
  return meets;
}
function objectification(json, timezone) {
  var meets = [];
  for (const day in json) {
    for (const time in json[day]) {
      let temp = new Object();
      temp.day = day;
      temp.numDay = dayNumber(day);
      temp.startTime = time.split(" - ")[0];
      temp.endTime = time.split(" - ")[1];
      temp.title = json[day][time].title;
      temp.app = json[day][time].app;
      temp.link = json[day][time].link;
      temp = convertToLocal(temp, timezone);

      if (typeof meets[temp.startTime + "- " + temp.endTime] === "undefined") {
        let dayObject = {};
        dayObject.title = temp.title;
        dayObject.app = temp.app;
        dayObject.link = temp.link;

        meets[temp.startTime + "- " + temp.endTime] = {};
        meets[temp.startTime + "- " + temp.endTime][temp.day] = dayObject;
      } else {
        let dayObject = {};
        dayObject.title = temp.title;
        dayObject.app = temp.app;
        dayObject.link = temp.link;
        meets[temp.startTime + "- " + temp.endTime][temp.day] = dayObject;
      }
    }
  }
  return meets;
}

function convertToLocal(meet, timezone, year = -1, month = -1, date = -1) {
  var hour = meet.startTime.split(":");
  var minutes = hour[1];
  hour = hour[0];
  if (year === -1) {
    var sourceDate = setFirstDayOfWeek(meet.numDay, timezone);
    month = sourceDate.getMonth() + 1;
    year = sourceDate.getFullYear();
    date = sourceDate.getDate();
  }

  function pad(n){return n<10 ? '0'+n : n}
  let newDate = moment
    .utc(year + "-" + pad(month) + "-" + pad(date) + " " + hour + ":" + minutes)
    .tz(timezone);
  meet.numDay = new Date(newDate.format().substring(0, 19)).getDay();
  meet.day = numToDay[meet.numDay];
  meet.startTime = newDate.format("HH:mm");
  hour = meet.endTime.split(":");
  minutes = hour[1];
  hour = hour[0];

  newDate = moment
    .utc(year + "-" + pad(month) + "-" + pad(date) + " " + hour + ":" + minutes)
    .tz(timezone);
  meet.endTime = newDate.format("HH:mm");
  return meet;
}
function setFirstDayOfWeek(numDay, timezone) {
  let format = moment.tz(timezone).format();
  var newDate = new Date(format.substring(0, 19));
  newDate.setDate(newDate.getDate() - newDate.getDay() + numDay);
  return newDate;
}

export default {
  name: "App",
  components: {
    MeetingCard,
  },
  data() {
    return {
      dayOfWeek: 0,
      listTimeZone: [],
      timeZoneSelect: "",
      meetingtimelist: [],
      meetingSpecial: [],
      meetingiemelistlenght: 10,
      showThisWeek: 0,
      weekDate: [],
      drawer: false,
      group: null,
      dialog: false,
      mobileDay: 0,
      dataNumToMonth: mobileNumToDay,
      weekPeriodString: "",
      clock: "",
    };
  },
  methods: {
    updateDateTime() {
      this.clock = moment.tz(this.timeZoneSelect).format("HH:mm:ss");
      this.$options.timer = window.setTimeout(this.updateDateTime, 1000);
    },
    sortOnKeys(dict) {
      var sorted = [];
      for (var key in dict) {
        sorted[sorted.length] = key;
      }
      sorted.sort();

      var tempDict = {};
      for (var i = 0; i < sorted.length; i++) {
        tempDict[sorted[i]] = dict[sorted[i]];
      }

      return tempDict;
    },
    specialToday(meet, str) {
      if (typeof meet === "undefined") {
        return false;
      }
      return numToMonth[meet.month - 1] + " " + meet.date === str;
    },
    nextMobileDay: function () {
      this.mobileDay++;
      if (this.mobileDay > 6) {
        this.mobileDay = 0;
      }
    },
    previousMobileDay: function () {
      this.mobileDay--;
      if (this.mobileDay < 0) {
        this.mobileDay = 6;
      }
    },
    nextWeek: function () {
      if (this.showThisWeek < this.meetingiemelistlenght - 1) {
        this.showThisWeek++;
      }
    },
    pervWeek: function () {
      if (this.showThisWeek > 0) {
        this.showThisWeek--;
      }
    },
    dayStatus: function (day, time) {
      if (day > this.dayOfWeek || this.showThisWeek > 0) {
        return "tomarow_card";
      }
      if (day < this.dayOfWeek) {
        return "lastday_card";
      }
      let format = moment.tz(this.timeZoneSelect).format();
      var newDate = new Date(format.substring(0, 19));

      time = time.split("- ")[0];
      if (time.split(":")[0] < newDate.getHours()) {
        return "lastday_card";
      }
      return "today_card";
    },
    getDayFromMeet: function (day) {
      var meetObject;
      var x = new Date(day);
      x.toString().split(" ");
      meetObject.dayOfWeek = x[0];
      meetObject.month = x[1];
      meetObject.dayOfMonth = x[2];
      meetObject.year = x[3];
      meetObject.time = x[4];
      meetObject.gmtOffset = x[5];
      return meetObject;
    },
  },
  created: function () {
    this.listTimeZone = moment.tz.names();
    this.timeZoneSelect = moment.tz.guess();
  },
  watch: {
    timeZoneSelect() {
      let format = moment.tz(this.timeZoneSelect).format();
      this.dayOfWeek = new Date(format.substring(0, 19)).getDay() - 1;
      if (this.dayOfWeek < 0) {
        this.dayOfWeek = 6;
      }
      this.mobileDay = this.dayOfWeek;
      var nowTime = new Date(format.substring(0, 19));
      nowTime.setDate(
        nowTime.getDate() - (nowTime.getDay() > 0 ? nowTime.getDay() - 1 : 6)
      );

      this.weekDate = sevenDayOfMonth(
        numToMonth[nowTime.getMonth()],
        nowTime.getDate(),
        nowTime.getFullYear()
      );
      var endDayOfThisWeek = new Date(format.substring(0, 19));
      endDayOfThisWeek.setDate(nowTime.getDate() + 7);
      this.weekPeriodString =
        numToMonth[nowTime.getMonth()] +
        " " +
        nowTime.getDate() +
        " - " +
        numToMonth[endDayOfThisWeek.getMonth()] +
        " " +
        endDayOfThisWeek.getDate() +
        "," +
        nowTime.getFullYear();

      axios.get("./weeklyBase.json").then((response) => {
        this.meetingtimelist = this.sortOnKeys(
          objectification(response.data, this.timeZoneSelect)
        );
      }),
        axios.get("./specialMeeting.json").then((response) => {
          this.meetingSpecial = this.sortOnKeys(
            objectificationSpecialTime(response.data, this.timeZoneSelect)
          );
        });
    },
    group() {
      this.drawer = false;
    },
    showThisWeek: function () {
      let format = moment.tz(this.timeZoneSelect).format();
      var nowTime = new Date(format.substring(0, 19));
      nowTime.setDate(
        nowTime.getDate() - (nowTime.getDay() > 0 ? nowTime.getDay() - 1 : 6)
      );
      nowTime.setDate(nowTime.getDate() + 7 * this.showThisWeek);
      var endDayOfThisWeek = new Date(format.substring(0, 19));
      endDayOfThisWeek.setDate(nowTime.getDate() + 7);
      this.weekPeriodString =
        numToMonth[nowTime.getMonth()] +
        " " +
        nowTime.getDate() +
        " - " +
        numToMonth[endDayOfThisWeek.getMonth()] +
        " " +
        endDayOfThisWeek.getDate() +
        "," +
        nowTime.getFullYear();

      this.weekDate = sevenDayOfMonth(
        numToMonth[nowTime.getMonth()],
        nowTime.getDate(),
        nowTime.getFullYear()
      );
    },
  },
  mounted() {
    this.$options.timer = window.setTimeout(this.updateDateTime, 1000);
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;700&display=swap");

.v-application {
  overflow-x: hidden;
}
.changefont,
.v-application,
.v-application .text-h3,
.v-application .text-h4,
.v-application .text-h5,
.v-application .text-h6 {
  font-family: "Poppins", sans-serif !important;
}
.v-application a {
  text-decoration: none;
  color: #ececec;
}

.v-application a:hover {
  color: #ed7a5d;
}

.navigation {
  background-color: white !important;
  box-shadow: none !important;
}

.header {
  background-image: url("./assets/Network illustration.png");
  height: 400px;
}
.theme--light.v-input input,
.theme--light.v-input textarea {
  color: blue !important;
}
.seven-col .col-1 {
  max-width: 12.5% !important;
  width: 12.5% !important;
  flex: none !important;
}
.day-week {
  border-bottom: 1px black solid;
}
.last_days {
  color: #bdbdbd;
}
.today h5 {
  color: #ed7a5d;
}
.today {
  border-bottom: none;
  position: relative;
}
.today_lable {
  position: absolute;
  bottom: -15;
  right: 0;
  left: 0;
}
.hand_icon {
  cursor: pointer;
}
.right_absolute {
  position: absolute !important;
  right: 0 !important;
}
.theme--dark.v-icon {
  color: black;
}
.footerstyle a {
  color: black;
}
.footerstyle a :hover {
  color: #ed7a5d !important;
}
</style>
