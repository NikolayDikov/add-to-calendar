<template>
    <div class='buttonContainer'>
        <div id="googlecalendarbrn" class="mrNext" @click="openGoogle(cinputJSON)">{{
          cinputJSON.GoogleButton
        }}</div>
        <!-- <div id="outlookcalendarbrn" class="mrNext" @click="openOutlook(cinputJSON)">{{
          cinputJSON.OutlookButton
        }}</div>
        <div id="o365calendarbrn" class="mrNext" @click="openOffice365(cinputJSON)">{{
          cinputJSON.O365Button
        }}</div> -->
        <div id="yahoocalendarbrn" class="mrNext" @click="openYahoo(cinputJSON)">{{
          cinputJSON.YahooButton
        }}</div>
        <div id="icalendarbrn" class="mrNext" @click="openIcs(cinputJSON)">{{
          cinputJSON.ICSButton
        }}</div>
    </div>
</template>

<script>
/* eslint no-undef: "warn" */
import { google, yahoo,  ics } from "calendar-link"; //outlook, office365,

export default {
  name: 'CalendarButtons',
  props: { cinputJSON: Object },
  methods: {
    openCalendar(url, ics) {
        if (!ics){
            var win = window.open(url,'_blank');
            win.focus();
        }
        else{
            console.log("save ics");
            this.saveICS(url);
        }
    
    },
    saveICS(fileURL){
        if (!window.ActiveXObject) {
            var save = document.createElement('a');
            save.href = fileURL;
            save.target = '_blank';
            save.download = "download.ics";
    
            var evt = new MouseEvent('click', {
                'view': window,
                'bubbles': true,
                'cancelable': false
            });
            save.dispatchEvent(evt);
    
            (window.URL || window.webkitURL).revokeObjectURL(save.href);
        }
    
        // for IE < 11
        else if ( !! window.ActiveXObject && document.execCommand)     {
            var _window = window.open(fileURL, '_blank');
            _window.document.close();
            _window.document.execCommand('SaveAs', true, this.fileName || fileURL)
            _window.close();
        }	
    },
    openGoogle(obj){
        let url= google(obj);
        $('.mrEdit').val($('.mrEdit').val() + 'Google calendar opened -#- ');
        this.openCalendar(url,false);
    },
    // openOutlook(obj){
    //     let url= outlook(obj);
    //     $('.mrEdit').val($('.mrEdit').val() + 'Outlook calendar opened -#- ');
    //     this.openCalendar(url,false);
    // },
    // openOffice365(obj){
    //     let url= office365(obj);
    //     $('.mrEdit').val($('.mrEdit').val() + 'Office365 calendar opened -#- ');
    //     this.openCalendar(url,false);
    // },
    openYahoo(obj){
        let url= yahoo(obj);
        $('.mrEdit').val($('.mrEdit').val() + 'Yahoo calendar opened -#- ');
        this.openCalendar(url,false);
    },
    openIcs(obj){
        let url= ics(obj);
        $('.mrEdit').val($('.mrEdit').val() + 'Ics calendar opened -#- ');
        this.openCalendar(url,true);
    }
  },
}
</script>

<style scoped>
.buttonContainer{
    display: flex;
    justify-content: space-evenly;
    flex-wrap: wrap;
    width: 90%;
    margin:auto;
}
.buttonContainer > div{
    margin: 5px;
    flex-grow: 1;
}

</style>