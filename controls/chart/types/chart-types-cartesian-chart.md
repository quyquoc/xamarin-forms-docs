---
title: Cartesian Chart
position: 1
slug: chart-types-cartesian-chart
---
# RadCartesianChart #
This chart visualizes its data points using the Cartesian coordinate system. The X and Y axes define how the coordinates of each point in the plot area are calculated and the series type define the way these data points will be visualized.  
![Cartesian Chart](/images/controls/chart/types/cartesian-chart-example.png)
## Supported Series ##
**RadCartesianChart** can visualize the following types of series:

- **LineSeries**: Visualizes a collection of data points using a line.
- **SplineSeries**: Visualizes a collection of data points using a curve.
- **AreaSeries**: Represents a chart series that are visualized like an area figure in the Cartesian space.
- **SplineAreaSeries**: Represents series which define an area with smooth curves among points.
- **BarSeries**: Represents a chart series that plot their points using rectangular shapes, named "Bars". 

## Supported Axes ##
**RadCartesianChart** needs to have two axes which will be used to calculate correctly the position of each data point. Usually one of the axes will be used to display the category of each data point and the other will represent its value. Here are the supported axes:

- **CategoricalAxis**: Arranges the plotted data points in categories where the key of each category is the point's value (if available) for that axis or its index within the points collection. The point's coordinate, specified by this axis is discrete and is calculated depending on the size of the category slot where the point resides.
- **NumericalAxis**: Calculates the coordinate of each data point, depending on the actual numerical value this point provides for the axis. A NumericalAxis exposes Minimum and Maximum properties to allow for explicit definition of the range of values visible on this axis. If these properties are not specified, the axis will automatically calculate the range, depending on the minimum and maximum data point values.- **DateTimeContinuousAxis**: This is a special axis that expects each data point to provide a DateTime structure as its value for this axis. You can think of DateTimeContinuousAxis as a timeline where the coordinate of each data point is calculated depending on the position of its associated DateTime on the timeline. The base unit (or the timeline step) of the axis is calculated depending on the smallest difference between any two dates.

## Example ##
1. Define RadCartesianChart:  
	
		XAML definition:
		<telerikChart:RadCartesianChart>
		</telerikChart:RadCartesianChart>

		C# definition:
		var chart = new RadCartesianChart();

1. The RadCartesianChart control needs two axes - horizontal and vertical to plot its data.

		XAML definition:
		<telerikChart:RadCartesianChart.HorizontalAxis>
		  <telerikChart:CategoricalAxis/>
		</telerikChart:RadCartesianChart.HorizontalAxis>
		<telerikChart:RadCartesianChart.VerticalAxis>
		  <telerikChart:NumericalAxis/>
		</telerikChart:RadCartesianChart.VerticalAxis>

		C# definition:
		chart.HorizontalAxis = new CategoricalAxis();
		chart.VerticalAxis = new NumericalAxis();

1. After that you can add the series to the RadCartesianChart.Series collection:

		XAML definition:
		<telerikChart:RadCartesianChart.Series>
		  <telerikChart:BarSeries ItemsSource="{Binding CategoricalData}">
		    <telerikChart:BarSeries.ValueBinding>
		      <telerikChart:PropertyNameDataPointBinding PropertyName="Value"/>
		    </telerikChart:BarSeries.ValueBinding>
		    <telerikChart:BarSeries.CategoryBinding>
		      <telerikChart:PropertyNameDataPointBinding PropertyName="Category"/>
		    </telerikChart:BarSeries.CategoryBinding>
		    </telerikChart:BarSeries>
		  </telerikChart:RadCartesianChart.Series>
		</telerikChart:RadCartesianChart>

		C# definition:
		var series = new BarSeries();
		series.SetBinding(BarSeries.ItemsSourceProperty, new Binding("CategoricalData"));
		series.ValueBinding = new PropertyNameDataPointBinding("Value");
		series.CategoryBinding = new PropertyNameDataPointBinding("Category");            
		chart.Series.Add(series);
1. You also have to set a BindingContext of the chart if none of its parents have a context:
 
		XAML definition:
		<telerikChart:RadPieChart.BindingContext>
		  <local:ViewModel/>
		</telerikChart:RadPieChart.BindingContext>

		C# definition:
		chart.BindingContext = new ViewModel();

Here is the full definition of the chart:

		<telerikChart:RadCartesianChart>
		  <telerikChart:RadPieChart.BindingContext>
		    <local:ViewModel/>
		  </telerikChart:RadPieChart.BindingContext>
		  <telerikChart:RadCartesianChart.HorizontalAxis>
		    <telerikChart:CategoricalAxis/>
		  </telerikChart:RadCartesianChart.HorizontalAxis>
		  <telerikChart:RadCartesianChart.VerticalAxis>
		    <telerikChart:NumericalAxis/>
		  </telerikChart:RadCartesianChart.VerticalAxis>
		  <telerikChart:RadCartesianChart.Series>
		    <telerikChart:BarSeries ItemsSource="{Binding CategoricalData}">
		      <telerikChart:BarSeries.ValueBinding>
		        <telerikChart:PropertyNameDataPointBinding PropertyName="Value"/>
		      </telerikChart:BarSeries.ValueBinding>
		      <telerikChart:BarSeries.CategoryBinding>
		        <telerikChart:PropertyNameDataPointBinding PropertyName="Category"/>
		      </telerikChart:BarSeries.CategoryBinding>
		    </telerikChart:BarSeries>
		  </telerikChart:RadCartesianChart.Series>
		</telerikChart:RadCartesianChart>

And this is the sample data

		public class CategoricalData
		{
		    public object Category { get; set; }
		
		    public double Value { get; set; }
		}

		public class ViewModel
		{
		    public ViewModel()
		    {
		        this.CategoricalData = GetCategoricalData();
		    }
		
		    public ObservableCollection<CategoricalData> CategoricalData { get; set; }
		
		    public static ObservableCollection<CategoricalData> GetCategoricalData()
		    {
		        var data = new ObservableCollection<CategoricalData>
		        {
		            new CategoricalData { Category = "A", Value = 0.63 },
		            new CategoricalData { Category = "B", Value = 0.85 },
		            new CategoricalData { Category = "C", Value = 0.75 },
		            new CategoricalData { Category = "D", Value = 0.96 },
		            new CategoricalData { Category = "E", Value = 0.78 },
		        };
		
		        return data;
		    }
		}