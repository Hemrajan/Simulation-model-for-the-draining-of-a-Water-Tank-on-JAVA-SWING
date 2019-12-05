# Simulation-model-for-the-draining-of-a-Water-Tank-on-JAVA-SWING


package turgun;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Random;

import javax.swing.text.StyledEditorKit.ForegroundAction;
import javax.swing.text.html.HTMLDocument.Iterator;

import com.sun.org.apache.xerces.internal.util.SynchronizedSymbolTable;

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.chart.CategoryAxis;
import javafx.scene.chart.LineChart;
import javafx.scene.chart.NumberAxis;
import javafx.scene.chart.ScatterChart;
import javafx.scene.chart.XYChart;
import javafx.stage.Stage;


import javax.swing.ComboBoxEditor;
import javax.swing.ComboBoxModel;
import javax.swing.JComboBox;
import javax.swing.JFrame;

import java.awt.*;
import java.awt.event.*;
import java.math.RoundingMode;
import java.text.DecimalFormat;

import javax.swing.*;
import javafx.scene.Scene;
import javafx.scene.chart.LineChart;
import javafx.scene.chart.NumberAxis;
import javafx.scene.chart.XYChart;
import javafx.stage.Stage;




public class WaterTank extends  Application{
	
	//int myArray[] = new int[30];
	double heightArray[] = new double[100];  // define differently 20 points
	double heightRKArray[] = new double[100];  // define differently 20 points
	double heightEAArray[] = new double[100];  // define differently 20 points
	double heightEA3StepArray[] = new double[100];  // define differently 20 points
	double heightPCStepArray[] = new double[100];  // define differently 20 points
	double d = 0.1;
	double D = 1.0;
	double h0 = 6.0;
	double g = 9.809;
	
	int[] steps = {1,2,5,10};
	//int[] stepsRK4 = {2,5,10};
	//double totalTime = Math.pow(d, 2)/Math.pow(D, 2)*Math.sqrt(2*h0/9); // taking total time during Flow water.
	
	// for The Fourth Order Runge Kutta Method
	int step = 5;
	double k1,k2,k3,k4;
	
	 @Override public void start(Stage stage) {
		 
	        stage.setTitle("By Aimirejiang TUERGAN");
	        //defining the axes
	        final NumberAxis xAxis = new NumberAxis();
	        final NumberAxis yAxis = new NumberAxis();
	        xAxis.setLabel("Time variables");
	        yAxis.setLabel("water Level variables");
	        //creating the chart
	        final LineChart<Number,Number> lineChart = new LineChart<Number,Number>(xAxis,yAxis);
	                
	        lineChart.setTitle(" Water Tank :  Informatics Engineering Faculty UTB ");
	        //defining a series
	        XYChart.Series series = new XYChart.Series();
	        XYChart.Series series1 = new XYChart.Series();
	        XYChart.Series series2 = new XYChart.Series();
      	    XYChart.Series series3 = new XYChart.Series();
      	    XYChart.Series series4 = new XYChart.Series();
      	    XYChart.Series series5 = new XYChart.Series();
      	    XYChart.Series series6 = new XYChart.Series();
      	    XYChart.Series series7 = new XYChart.Series();
      	    XYChart.Series series8 = new XYChart.Series();
      	    XYChart.Series series9 = new XYChart.Series();
      	    XYChart.Series series10 = new XYChart.Series();
      	    XYChart.Series series11 = new XYChart.Series();
      	    XYChart.Series series12 = new XYChart.Series();
      	    XYChart.Series series13 = new XYChart.Series();
      	    XYChart.Series series14 = new XYChart.Series();
      	    XYChart.Series series15 = new XYChart.Series();
	        // Water tank Elure Mathod
	        // draw graph	       
      	  DecimalFormat df = new DecimalFormat("#.########");
      	  df.setRoundingMode(RoundingMode.CEILING);
      	    double Ht = 0.00;
	        for (int stepSize : steps) {
	            System.out.println ("Step size: " + stepSize);
		            if(stepSize == 1)
		            { 
		            	
		            	System.out.println("Euler Step Size 1");
		    	        series.setName("Euler Step "+stepSize);
		    	        double Hn = h0;
		    	        double Hnext = 0.0;
		    	        heightArray[0] = h0;
		    	        int j=0;
		    	        for(int i = 1; i<heightArray.length ; i++)
		    	        {
		    	        	Hnext = Hn+stepSize*(-Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn));
		    	        	Hn = Hnext;
		    	        	heightArray[i] = Hnext;
		    	        	j += stepSize;   // time iterate
		    	        	
		    	        	// Analytical solution 
		    	        	Ht = Math.pow((-Math.sqrt(g/2)*(Math.pow(d, 2)/Math.pow(D, 2))*stepSize*Math.sqrt(Hn)),2);
		    	        	
		    	        	System.out.println(j+" "+heightArray[i]);
		    	        	//System.out.println(df.format(Ht));
		    	        	
		    	        	series.getData().add(new XYChart.Data(j, heightArray[i]));
		    	        	if(Hnext < 0)
		    	        		break;
		    	        }
		    	        System.out.println("RK4 Step Size"+stepSize);
		        		series1.setName("RK4 Step"+stepSize);
		    	        Hn = h0;
		    	        Hnext = 0.0;
		    	        heightRKArray[0] = h0;
		    	        int st = 0;
				        for(int i = 1; i<heightRKArray.length ; i++)
				        {
				        	k1 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn);
				        	k2 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+stepSize/2*k1);
				        	k3 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+stepSize/2*k2);
				        	k4 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+stepSize*k3);
				        	// algorthims
				        	Hnext = Hn+stepSize*(k1/6+k2/3+k3/3+k4/6);
				        	Hn = Hnext;
				        	heightRKArray[i] = Hnext;
				        	
				        	st += stepSize;
				        	System.out.println(st+" "+Hnext);
				        	series1.getData().add(new XYChart.Data(st, heightRKArray[i]));
				        	if( st == 100)
				        		break;
				        }
				        System.out.println("EAM Step Size"+stepSize);
				        series2.setName("EAM steps"+stepSize);
		    	        Hn = h0;
		    	        Hnext = 0.0;
		    	        heightEAArray[0] = h0;
		    	        int stp = 0; 
				        for(int i = 1; i<heightEAArray.length ; i++)
				        {
				        	 double fun = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn);
				    	     double fun2 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+0.001);
				        	// algorthims
				        	Hnext = Hn+stepSize*fun;
				        	Hn = Hnext;
				        	heightEAArray[i] = Hnext;
				        	stp += stepSize;
				        	System.out.println(stp+" -> "+heightEAArray[i]);
				        	series2.getData().add(new XYChart.Data(stp, heightEAArray[i]));
				        	if(Hnext < 0)
				        		break;
				        }
				        System.out.println("PC-Pre Size :"+stepSize);
			        	series3.setName("PC-Pre"+stepSize);
		    	        double H = h0;
		    	        double Hnxt1 = 0.0;
		    	        double Hnxt2 = 0.0;
		    	        heightEA3StepArray[0]=h0;
		    	        int stps =0;
		    	        double h1 = 0.00;
				        for(int i = 1; i<heightEA3StepArray.length	; i++)
				        {
				        	h1 = H+stepSize*(-Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(H));
			    	        double f = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(H);
			    	        double f2 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(h1);
			    	       double f3 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(H+0.20);
			    	        
			    	       Hnxt1 = h1+stepSize/2*(3*(f2)-(f));
			    	       Hnxt2 = h1+stepSize/12*(5*(-Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hnxt1))+8*(f2)-(f));
			    	       H = Hnxt2;
			    	       // algorthims
			    	      
;
				        	heightEA3StepArray[i] = Hnxt2;
				        	//System.out.println(Hnxt1+" "+Hnxt2);
				        	stps += stepSize;
				        	System.out.println(stps + " "+Hnxt2);
				        	series3.getData().add(new XYChart.Data(stps,Hnxt2));

				        	if (heightEA3StepArray[i] <0.00 || stps == 90 )
				        		break;
				        	
				        }  
		            } 
		            
		            if(stepSize == 2)
		            { 
		            	
		            	System.out.println("Euler Step Size :"+stepSize);
		    	        series4.setName("Euler Step "+stepSize);
		    	        double Hn = h0;
		    	        double Hnext = 0.0;
		    	        heightArray[0] = h0;
		    	        int j=0;
		    	        for(int i = 1; i<heightArray.length ; i++)
		    	        {
		    	        	Hnext = Hn+stepSize*(-Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn));
		    	        	Hn = Hnext;
		    	        	heightArray[i] = Hnext;
		    	        	j += stepSize;   // time iterate
		    	        	
		    	        	// Analytical solution 
		    	        	Ht = Math.pow((-Math.sqrt(g/2)*(Math.pow(d, 2)/Math.pow(D, 2))*stepSize*Math.sqrt(Hn)),2);
		    	        	
		    	        	System.out.println(j+" "+heightArray[i]);
		    	        	//System.out.println(df.format(Ht));
		    	        	
		    	        	series4.getData().add(new XYChart.Data(j, heightArray[i]));
		    	        	if(Hnext < 0)
		    	        		break;
		    	        }
		    	        System.out.println("RK4 Step Size"+stepSize);
		        		series5.setName("RK4 Step"+stepSize);
		    	        Hn = h0;
		    	        Hnext = 0.0;
		    	        heightRKArray[0] = h0;
		    	        int st = 0;
				        for(int i = 1; i<heightRKArray.length ; i++)
				        {
				        	k1 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn);
				        	k2 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+stepSize/2*k1);
				        	k3 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+stepSize/2*k2);
				        	k4 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+stepSize*k3);
				        	// algorthims
				        	Hnext = Hn+stepSize*(k1/6+k2/3+k3/3+k4/6);
				        	Hn = Hnext;
				        	heightRKArray[i] = Hnext;
				        	
				        	st += stepSize;
				        	System.out.println(st+" "+Hnext);
				        	series5.getData().add(new XYChart.Data(st, heightRKArray[i]));
				        	if( st == 100)
				        		break;
				        }
				        System.out.println("EAM Step Size"+stepSize);
				        series6.setName("EAM steps"+stepSize);
		    	        Hn = h0;
		    	        Hnext = 0.0;
		    	        heightEAArray[0] = h0;
		    	        int stp = 0; 
				        for(int i = 1; i<heightEAArray.length ; i++)
				        {
				        	 double fun = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn);
				    	     double fun2 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+0.001);
				        	// algorthims
				        	Hnext = Hn+stepSize*fun;
				        	Hn = Hnext;
				        	heightEAArray[i] = Hnext;
				        	stp += stepSize;
				        	System.out.println(stp+" -> "+heightEAArray[i]);
				        	series6.getData().add(new XYChart.Data(stp, heightEAArray[i]));
				        	if(Hnext < 0)
				        		break;
				        }
				        System.out.println("PC-Pre Size :"+stepSize);
			        	series7.setName("PC-Pre"+stepSize);
		    	        double H = h0;
		    	        double Hnxt1 = 0.0;
		    	        double Hnxt2 = 0.0;
		    	        heightEA3StepArray[0]=h0;
		    	        int stps =0;
		    	        double h1 = 0.00;
				        for(int i = 1; i<heightEA3StepArray.length	; i++)
				        {
				        	h1 = H+stepSize*(-Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(H));
			    	        double f = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(H);
			    	        double f2 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(h1);
			    	       double f3 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(H+0.20);
			    	        
			    	       Hnxt1 = h1+stepSize/2*(3*(f2)-(f));
			    	       Hnxt2 = h1+stepSize/12*(5*(-Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hnxt1))+8*(f2)-(f));
			    	       H = Hnxt2;
			    	       // algorthims
			    	      
;
				        	heightEA3StepArray[i] = Hnxt2;
				        	//System.out.println(Hnxt1+" "+Hnxt2);
				        	stps += stepSize;
				        	System.out.println(stps + " "+Hnxt2);
				        	series7.getData().add(new XYChart.Data(stps,Hnxt2));

				        	if (heightEA3StepArray[i] <0.00 || stps == 90 )
				        		break;
				        	
				        }  
		            }   
		            if(stepSize == 5)
		            { 
		            	
		            	System.out.println("Euler Step Size:"+stepSize);
		    	        series8.setName("Euler Step "+stepSize);
		    	        double Hn = h0;
		    	        double Hnext = 0.0;
		    	        heightArray[0] = h0;
		    	        int j=0;
		    	        for(int i = 1; i<heightArray.length ; i++)
		    	        {
		    	        	Hnext = Hn+stepSize*(-Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn));
		    	        	Hn = Hnext;
		    	        	heightArray[i] = Hnext;
		    	        	j += stepSize;   // time iterate
		    	        	
		    	        	// Analytical solution 
		    	        	Ht = Math.pow((-Math.sqrt(g/2)*(Math.pow(d, 2)/Math.pow(D, 2))*stepSize*Math.sqrt(Hn)),2);
		    	        	
		    	        	System.out.println(j+" "+heightArray[i]);
		    	        	//System.out.println(df.format(Ht));
		    	        	
		    	        	series8.getData().add(new XYChart.Data(j, heightArray[i]));
		    	        	if(Hnext < 0)
		    	        		break;
		    	        }
		    	        System.out.println("RK4 Step Size "+stepSize);
		        		series9.setName("RK4 Step"+stepSize);
		    	        Hn = h0;
		    	        Hnext = 0.0;
		    	        heightRKArray[0] = h0;
		    	        int st = 0;
				        for(int i = 1; i<heightRKArray.length ; i++)
				        {
				        	k1 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn);
				        	k2 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+stepSize/2*k1);
				        	k3 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+stepSize/2*k2);
				        	k4 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+stepSize*k3);
				        	// algorthims
				        	Hnext = Hn+stepSize*(k1/6+k2/3+k3/3+k4/6);
				        	Hn = Hnext;
				        	heightRKArray[i] = Hnext;
				        	
				        	st += stepSize;
				        	System.out.println(st+" "+Hnext);
				        	series9.getData().add(new XYChart.Data(st, heightRKArray[i]));
				        	if( st == 100)
				        		break;
				        }
				        System.out.println("EAM Step Size "+stepSize);
				        series10.setName("EAM "+stepSize);
		    	        Hn = h0;
		    	        Hnext = 0.0;
		    	        heightEAArray[0] = h0;
		    	        int stp = 0; 
				        for(int i = 1; i<heightEAArray.length ; i++)
				        {
				        	 double fun = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn);
				    	     double fun2 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+0.001);
				        	// algorthims
				        	Hnext = Hn+stepSize*fun;
				        	Hn = Hnext;
				        	heightEAArray[i] = Hnext;
				        	stp += stepSize;
				        	System.out.println(stp+" -> "+heightEAArray[i]);
				        	series10.getData().add(new XYChart.Data(stp, heightEAArray[i]));
				        	if(Hnext < 0)
				        		break;
				        }
				        System.out.println("PC-Pre Size :"+stepSize);
			        	series11.setName("PC-Pre"+stepSize);
		    	        double H = h0;
		    	        double Hnxt1 = 0.0;
		    	        double Hnxt2 = 0.0;
		    	        heightEA3StepArray[0]=h0;
		    	        int stps =0;
		    	        double h1 = 0.00;
				        for(int i = 1; i<heightEA3StepArray.length	; i++)
				        {
				        	h1 = H+stepSize*(-Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(H));
			    	        double f = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(H);
			    	        double f2 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(h1);
			    	       double f3 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(H+0.20);
			    	        
			    	       Hnxt1 = h1+stepSize/2*(3*(f2)-(f));
			    	       Hnxt2 = h1+stepSize/12*(5*(-Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hnxt1))+8*(f2)-(f));
			    	       H = Hnxt2;
			    	       // algorthims
			    	      
;
				        	heightEA3StepArray[i] = Hnxt2;
				        	//System.out.println(Hnxt1+" "+Hnxt2);
				        	stps += stepSize;
				        	System.out.println(stps + " "+Hnxt2);
				        	series11.getData().add(new XYChart.Data(stps,Hnxt2));

				        	if (heightEA3StepArray[i] <0.00 || stps == 90 )
				        		break;
				        	
				        }  
		            } 
		            
		            if(stepSize == 10)
		            { 
		            	
		            	System.out.println("Euler Step Size "+stepSize);
		    	        series12.setName("Euler Step"+stepSize);
		    	        double Hn = h0;
		    	        double Hnext = 0.0;
		    	        heightArray[0] = h0;
		    	        int j=0;
		    	        for(int i = 1; i<heightArray.length ; i++)
		    	        {
		    	        	Hnext = Hn+stepSize*(-Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn));
		    	        	Hn = Hnext;
		    	        	heightArray[i] = Hnext;
		    	        	j += stepSize;   // time iterate
		    	        	
		    	        	// Analytical solution 
		    	        	Ht = Math.pow((-Math.sqrt(g/2)*(Math.pow(d, 2)/Math.pow(D, 2))*stepSize*Math.sqrt(Hn)),2);
		    	        	
		    	        	System.out.println(j+" "+heightArray[i]);
		    	        	//System.out.println(df.format(Ht));
		    	        	
		    	        	series12.getData().add(new XYChart.Data(j, heightArray[i]));
		    	        	if(Hnext < 0)
		    	        		break;
		    	        }
		    	        System.out.println("RK4 Step Size:"+stepSize);
		        		series13.setName("RK4 Step "+stepSize);
		    	        Hn = h0;
		    	        Hnext = 0.0;
		    	        heightRKArray[0] = h0;
		    	        int st = 0;
				        for(int i = 1; i<heightRKArray.length ; i++)
				        {
				        	k1 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn);
				        	k2 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+stepSize/2*k1);
				        	k3 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+stepSize/2*k2);
				        	k4 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+stepSize*k3);
				        	// algorthims
				        	Hnext = Hn+stepSize*(k1/6+k2/3+k3/3+k4/6);
				        	Hn = Hnext;
				        	heightRKArray[i] = Hnext;
				        	
				        	st += stepSize;
				        	System.out.println(st+" "+Hnext);
				        	series13.getData().add(new XYChart.Data(st, heightRKArray[i]));
				        	if( st == 100)
				        		break;
				        }
				        System.out.println("EAM Step Size "+stepSize);
				        series14.setName("EAM steps:"+stepSize);
		    	        Hn = h0;
		    	        Hnext = 0.0;
		    	        heightEAArray[0] = h0;
		    	        int stp = 0; 
				        for(int i = 1; i<heightEAArray.length ; i++)
				        {
				        	 double fun = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn);
				    	     double fun2 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hn+0.001);
				        	// algorthims
				        	Hnext = Hn+stepSize*fun;
				        	Hn = Hnext;
				        	heightEAArray[i] = Hnext;
				        	stp += stepSize;
				        	System.out.println(stp+" -> "+heightEAArray[i]);
				        	series14.getData().add(new XYChart.Data(stp, heightEAArray[i]));
				        	if(Hnext < 0)
				        		break;
				        }
				        System.out.println("PC-Pre Size :"+stepSize);
			        	series15.setName("PC-Pre"+stepSize);
		    	        double H = h0;
		    	        double Hnxt1 = 0.0;
		    	        double Hnxt2 = 0.0;
		    	        heightEA3StepArray[0]=h0;
		    	        int stps =0;
		    	        double h1 = 0.00;
				        for(int i = 1; i<heightEA3StepArray.length	; i++)
				        {
				        	h1 = H+stepSize*(-Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(H));
			    	        double f = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(H);
			    	        double f2 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(h1);
			    	       double f3 = -Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(H+0.20);
			    	        
			    	       Hnxt1 = h1+stepSize/2*(3*(f2)-(f));
			    	       Hnxt2 = h1+stepSize/12*(5*(-Math.sqrt(2*g)*(Math.pow(d, 2)/Math.pow(D, 2))*Math.sqrt(Hnxt1))+8*(f2)-(f));
			    	       H = Hnxt2;
			    	       // algorthims
			    	      
;
				        	heightEA3StepArray[i] = Hnxt2;
				        	//System.out.println(Hnxt1+" "+Hnxt2);
				        	stps += stepSize;
				        	System.out.println(stps + " "+Hnxt2);
				        	series15.getData().add(new XYChart.Data(stps,Hnxt2));

				        	if (heightEA3StepArray[i] <0.00 || stps == 90 )
				        		break;
				        	
				        }  
		            }
	        }
	        Scene scene  = new Scene(lineChart,1400,700);
	        lineChart.getData().addAll(series,series1,series2,series3,series4,series5,series6,series7,series8,series9,series10,series11,series12,series13,series14,series15);
	        stage.setScene(scene);
	        stage.show();
    }
		public static void main(String[] args){
			launch(args);
			
		}
}

