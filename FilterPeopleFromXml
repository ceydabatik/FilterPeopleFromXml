using System;
using System.Linq;
using System.Xml.Linq;
using System.Text.Json;

public class Program
{
    public static string FilterPeopleFromXml(string xmlData)
    {
        var doc = XDocument.Parse(xmlData);

        var query = doc.Descendants("Person")
            .Select(p => new
            {
                Name = (string)p.Element("Name"),
                Age = (int)p.Element("Age"),
                Department = (string)p.Element("Department"),
                Salary = (decimal)p.Element("Salary"),
                HireDate = DateTime.Parse((string)p.Element("HireDate"))
            })
            .Where(p => p.Age > 30 &&
                        p.Department == "IT" &&
                        p.Salary > 5000 &&
                        p.HireDate.Year < 2019)
            .OrderBy(p => p.Name)
            .ToList();

        var result = new
        {
            Names = query.Select(p => p.Name).ToList(),
            TotalSalary = query.Sum(p => p.Salary),
            AverageSalary = query.Count() > 0 ? query.Average(p => p.Salary) : 0,
            MaxSalary = query.Count() > 0 ? query.Max(p => p.Salary) : 0,
            Count = query.Count()
        };

        return JsonSerializer.Serialize(result);
    }

    // Test için Main metodu
    public static void Main()
    {
        string xml = @"
        <People>
            <Person>
                <Name>Alice</Name>
                <Age>35</Age>
                <Department>IT</Department>
                <Salary>6000</Salary>
                <HireDate>2015-03-10</HireDate>
            </Person>
            <Person>
                <Name>Bob</Name>
                <Age>28</Age>
                <Department>HR</Department>
                <Salary>4000</Salary>
                <HireDate>2020-01-15</HireDate>
            </Person>
            <Person>
                <Name>Charlie</Name>
                <Age>40</Age>
                <Department>IT</Department>
                <Salary>8000</Salary>
                <HireDate>2010-06-20</HireDate>
            </Person>
        </People>";

        string jsonResult = FilterPeopleFromXml(xml);
        Console.WriteLine(jsonResult);
    }
}
