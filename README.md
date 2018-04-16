# Mobile-Hybrid-Tools
Mobile hybrid developments for Ionic, cordova, phonegap

## Overview

- [Ionic SetTimeout/SetInterval when app is in background.](#Ionic-settimeout-setinterval-background)



#### Ionic setTimeout-SetInterval background.

In this case when app went in background mode the app is stopped as interaval or timeout. We use webview which doesn't give as opportunity to make timer. Ofcourse I could wrote pluign in Java or Swift but why not use javascript in this case it will be TypeScript because we use Ionic (but it won't matter). 


The maximum value of a signed 32 bit integer in ms. If it would be unsigned it would be 232-1 = 4,294,967,295.(Maxium value which can be manage by settimemout or setinterval).

This example is  for demonstrate not for exactly purpose to use.


In Main class you need to have these:

      //Make sure to import Platform from ionic-angular and Subscription from rxjs
      import { IonicPage, NavController, Platform } from 'ionic-angular';
      import { Subscription } from 'rxjs';
      
      
     //It can be also app.ts <-- root of entire project, 
    export class MainPage { 
      private onResumeSubscription: Subscription;   //Subscription 
      
      //for testing purpose
      private synch_tiemout= null;     
    
    // In constructor we set subscribion when app is resumed.
       constructor(public navCtrl: NavController, private platform: Platform) {
     
      this.onResumeSubscription = platform.resume.subscribe(() => {
            // Here we set the function which will be called to recaluclated Interval
            // Ex:
            this.synch_New_Data();
       });
      }
        
         //When app is closed
         ngOnDestroy(): void {
              this.onResumeSubscription.unsubscribe();
            }
          
          
         private synch_New_Data(){
              //cleanSettimeout if exist
               if (this.synch_tiemout != null) {
                   clearTimeout(this.synch_tiemout);
                 } 
                       let now = new Date();
                      //last_synch is var which is savaed to user data when was last synchronisation.                                              
                      //We recalculate time to synchonisation and we set again.
                      //Also is necessary to check if number is under 0.
                       let time_to_synch = ( now.getTime() - new Date(lastsynch).getTime() )

            this.synch_tiemout = settimeout(() => {
            
                  }, time_to_synch ) ;

          }
    }
   
