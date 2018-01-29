// Neural-Network BackPropagation Example code
#include<iostream>
#include<cstdlib>
#include<math.h>

using namespace std;

int main(int, char**)
{  

    /************************       Initialization  ******************************/  
    	double weight[2]={1.5,2.0};
    	double weight1[2]={2.5,3.0};
    	double weight2[2]={4.0,4.5};
    	double weight3[2]={5.0,5.5};
    	
    	double bias=0.35,bias_n=0.60;
    	double target[]={0,1};
    	double z[2],z1[2],z2[2],z3[2],sig[4],sig_m[4],error[2],error1[2],err;
    
        cout<<"INITIALIZED WEIGHTS : \n";
        cout<<"weight[1]: "<<weight[0]<<"\n"<<"weight[2]: "<<weight[1]<<"\n"<<"weight[3]: "<<weight1[0]<<"\n"<<"weight[4]: "<<weight1[1]<<"\n";
  	cout<<"weight[5]: "<<weight2[0]<<"\n""weight[6]: "<<weight2[1]<<"\n"<<"weight[7]: "<<weight3[0]<<"\n"<<"weight[8]: "<<weight3[1]<<"\n\n";
      
    
    /**************************** Hidden Layer  **********************************/
   	 for(int k=0;k<1000000;k++)
 	   {
            
                 double x[2]={1,0};                                         // Input.....
                 double sum[4]={0,0,0,0};
        	
                 for(int i=0;i<2;i++)
         	   {    

        		 z[i]= { weight[i] * x[i] };
       			 z1[i]= { weight1[i] * x[i] };
        		 sum[0]=sum[0]+z[i];
        		 sum[1]=sum[1]+z1[i];
        	   }      
       
     		 sum[0]=sum[0]+bias;
    		 sum[1]=sum[1]+bias;
     
    /*************************  Sigmoid function  ***********************************/
     

        	for(int j=0; j<1 ;j++)
        	{   
       		        sig[0]= (1 /( 1 + exp(-sum[0]) )) ;                       
            		sig[1]= (1 /( 1 + exp(-sum[1]) )) ;
          	        sig_m[0] = sig[0] * ( 1 - sig[0]) ;
            	        sig_m[1] = sig[1] * ( 1 - sig[1]) ;
     
                        
    /************************ Second Layer ****************************************/
         		  double h1[2]={sig[0], sig[1]};
           		for(int i=0;i<2;i++)
       	  			{    

        	 	      		z2[i]= { weight2[i] * h1[i] };
       					z3[i]= { weight3[i] * h1[i] };
        	 			sum[2]=sum[2]+z2[i];
        	 			sum[3]=sum[3]+z3[i];
           			}     
        		   
                            sum[2]=sum[2]+bias_n;
         		    sum[3]=sum[3]+bias_n;

          			
                            for(int j=0; j<1 ;j++)
        			{   
           				 sig[2]= (1 /( 1 + exp(-sum[2]) )) ;                       
            				 sig[3]= (1 /( 1 + exp(-sum[3]) )) ;
            				 sig_m[2] = sig[2] * ( 1 - sig[2]) ;
	    				 sig_m[3] = sig[3] * ( 1 - sig[3]) ;
        			}
                      
	        }
    

 /**************************** Error Calculation  *******************************/ 
        
         for(int k=0;k<1;k++)                                 
             {   
                  
                  error[k]=0.5*pow((target[k]-sig[2]),2);
                  error1[k]=0.5*pow((target[k+1]-sig[3]),2);
             
            }
    
  
 /*************************** Prining Error  ******************************/ 
     
       for(int l=0;l<1;l++)                                  
            {  
                   
                   err=error[l]+error1[l];
                  
            }
     

     if (err < pow(10,-10))                                                                // Checking error Limit ..... 
           {
                 
                 std::cout<<"Total Error:"<<err<<"\n\n";
 
          	 cout<<"UPDATED NEW WEIGHTS :\n";                                          // Final Output .....         
          	 cout<<"weight[1]: "<<weight[0]<<"\n"<<"weight[2]: "<<weight[1]<<"\n"<<"weight[3]: "<<weight1[0]<<"\n"<<"weight[4]: "<<weight1[1]<<"\n";
          	 cout<<"weight[5]: "<<weight2[0]<<"\n""weight[6]: "<<weight2[1]<<"\n"<<"weight[7]: "<<weight3[0]<<"\n"<<"weight[8]: "<<weight3[1]<<"\n";
	  
          	 cout<<"\nCALCULATED :\n   OUTPUT_1 :"<<sig[2]<<"\t\t"<<"OUTPUT_2: "<<sig[3]<<"\n\n";
          	 cout<<"EXPECTED  :\n   OUTPUT_1 :"<<target[0]<<"\t\t"<<"OUTPUT_2: "<<target[1]<<"\n";
          	 return 1;
           }

  /************************* Updating New Weights ******************************/
     
        weight[0]=weight[0]- ((0.1) * (((sig[2]-target[0])*(sig_m[2])*weight2[0]) + ((sig[3]-target[1])*sig_m[3]*weight3[0])) * sig_m[0] * x[0]);
       
        weight[1]=weight[1]- ((0.1) * (((sig[2]-target[0])*(sig_m[2])*weight2[0]) + ((sig[3]-target[1])*sig_m[3]*weight3[0])) * sig_m[0] * x[1]);
       
        weight1[0]=weight1[0]- ((0.1)* (( (sig[2]-target[0])*(sig_m[2])*weight2[1]) + ((sig[3]-target[1])*sig_m[3]*weight3[1])) * sig_m[1] * x[0]);

        weight1[1]=weight1[1] - ((0.1)*(( (sig[2]-target[0])*(sig_m[2])*weight2[1]) + ((sig[3]-target[1])*sig_m[3]*weight3[1])) * sig_m[1] * x[1]);
        
        
        weight2[0]=weight2[0]-((0.1)*((sig[0])*(sig_m[2])*(sig[2]-target[0])));
  
        weight2[1]=weight2[1]-((0.1)*((sig[1])*(sig_m[2])*(sig[2]-target[0])));
       
        weight3[0]=weight3[0]-((0.1)*((sig[0])*(sig_m[3])*(sig[3]-target[1])));
       
        weight3[1]=weight3[1]-((0.1)*((sig[1])*(sig_m[3])*(sig[3]-target[1])));
    
       
     
      
 
          
 }
          
   /************************* Final Output  *********************************/
           std::cout<<"Total Error:"<<err<<"\n\n";
 
           cout<<"UPDATED NEW WEIGHTS :\n";
           cout<<"weight[1]: "<<weight[0]<<"\n"<<"weight[2]: "<<weight[1]<<"\n"<<"weight[3]: "<<weight1[0]<<"\n"<<"weight[4]: "<<weight1[1]<<"\n";
           cout<<"weight[5]: "<<weight2[0]<<"\n""weight[6]: "<<weight2[1]<<"\n"<<"weight[7]: "<<weight3[0]<<"\n"<<"weight[8]: "<<weight3[1]<<"\n";
	  
           cout<<"\nCALCULATED :\n   OUTPUT_1 :"<<sig[2]<<"\t\t"<<"OUTPUT_2: "<<sig[3]<<"\n\n";
           cout<<"EXPECTED  :\n   OUTPUT_1 :"<<target[0]<<"\t\t"<<"OUTPUT_2: "<<target[1]<<"\n";

  return 0;

}































   
     
