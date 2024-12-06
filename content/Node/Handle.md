---
customer:
user:
status: closed
tags:
  - Issue
type: Issue
subject:
archived: true
---
Handle

```cs
using System;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Interop;
using EnhancedCard.ViewModels;

namespace EnhancedCard.Views
{
	/// <summary>
	/// Interaction logic for View1.xaml
	/// </summary>
	public partial class MainView : UserControl
	{
		public MainView()
		{
			InitializeComponent();
		}

		public IntPtr Handle
		{
			get
			{
				// Get the window that contains this UserControl
				Window window = Window.GetWindow(this);
				if (window == null)
					throw new InvalidOperationException("The UserControl is not hosted in a window.");

				// Use WindowInteropHelper to get the handle
				WindowInteropHelper helper = new WindowInteropHelper(window);
				return helper.Handle;
			}
		}
	}
}
```
