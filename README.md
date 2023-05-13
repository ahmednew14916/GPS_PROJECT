void recieved_string(char stop_char){
  char recieved_char=0;
	char i=0;
	while(recieved_char!=stop_char){
		recieved_char=UART5_read();
		if(recieved_char!=stop_char) {
			recieved_arr[i]=recieved_char;
		}
		i++;
	}
}




void gps_read(){
	char i=0;
	do{
		while(UART5_read()!=GPS_logName[i]);
		i++;
	}while(i!=6);
	recieved_string(',');
	copy_string(recieved_arr,"");
	recieved_string(',');
	if(strcmp_by_me(recieved_arr,"A")==0){
		copy_string(recieved_arr,"");
		recieved_string(',');
		currentLat=atof(recieved_arr);
		copy_string(recieved_arr,"");
		recieved_string(',');
		copy_string(recieved_arr,"");
		recieved_string(',');
    currentLong=atof(recieved_arr);
		copy_string(recieved_arr,"");
		recieved_string(',');
		copy_string(recieved_arr,"");
		recieved_string(',');
		speed=atof(recieved_arr);
	}
}
