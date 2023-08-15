# Automatic-Pet-feeder
It is a PIC 18 based device that automatically provides food to the pet by setting an alarm.

CODE

#include <p18f46k22.h>    
#include <stdio.h> 
#include <string.h>	
#include <stdlib.h>
#include "ProjectMain.h"  
#include "serial_codes.h"
#include "ADC.H" 
#include "PinAllocation.h"
#include "LCD.h"
#include "delay.h"
#include "timers.h"
#include "wifimodule.h" 

unsigned char guchValueFromUART1;
unsigned int gunLMData;
unsigned int gunLMData1;
unsigned char garruchTempLCDDisplay[17]; 
unsigned char guchLCDLine1String[17],guchLCDLine2String[17];
unsigned char uchBuffDisplay[] = "APSIS SOLUTIONS\n\r";
#pragma udata udata3
unsigned char uchRecieve150Ch[150],i = 0;
unsigned int guchDataTowebsite;
extern unsigned int gunField1Value,gunField2Value,gunField3Value,gunField4Value,gunField5Value,gunField6Value,gunField7Value,gunField8Value;
unsigned long ulVoltageInVolts;
extern unsigned char guchField5Value;
extern unsigned int gunDataFromFields;
unsigned char guchSendingData[10]= "TESTED OK";
unsigned int gunValueFromADC;
unsigned char gunBTData[15]={"BTSendingData"};

void fnMotor_1_Stop(void)
{
	MOTOR_1_COIL_A = 0;
	MOTOR_1_COIL_B = 0;
	
}

void fnMotor_1_Clk(void)
{
	MOTOR_1_COIL_A = 0;
	MOTOR_1_COIL_B = 1;
	EN_1 =0;
	
}

void fnMotor_1_AntiClk(void)
{
	MOTOR_1_COIL_A = 1;
	MOTOR_1_COIL_B = 0;
	EN_1 =0;
	
}






void fnMain_Project()
{	
	unsigned int unTemperatureValue; 
	unsigned int unADCvalueSmokeSensor =0;
	unsigned int unDataFromThingspeakforDeviceControl = 0;
	unsigned int unDataFromField1,unDataFromField2;
	unsigned char uchCommandForRobot;
	unsigned char a=10,b=5,c=0;
	unsigned char uchData;
	unsigned char uchData1;
	
 	unsigned char uchRecieve150Ch[10],i = 0;
 	unsigned char uchtemp;
 	
 	unsigned char uchTempvalue[];
 	unsigned int  unADCvalue1=0;
 	unsigned int  unADCvalue2=0;
 	unsigned int  unADCvalue3=0;
 	unsigned int  unADCvalue4=0;




	ANS_MOTOR_1_COIL_A = SET_DIGITAL;
	ANS_MOTOR_1_COIL_B = SET_DIGITAL;
	ANS_EN_1=SET_DIGITAL;
	
	
	DIR_MOTOR_1_COIL_A = SET_OUTPUT;
	DIR_MOTOR_1_COIL_B = SET_OUTPUT;
	DIR_EN_1=SET_OUTPUT;
    




	while(1)
	{
		guchValueFromUART1 = uchfnReceive_Serial(UART1);
		printf("%c %d 0x%X\n",guchValueFromUART1,guchValueFromUART1,guchValueFromUART1);
		
		if(guchValueFromUART1 == 'F')
		{
		fnMotor_1_Clk();	
		}
		else if(guchValueFromUART1 == 'B')
		{
		fnMotor_1_AntiClk();	
		}
		
		else
		{
			fnMotor_1_Stop();
		}

	}

