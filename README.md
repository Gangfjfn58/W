# W
Canada 
import { useState, useEffect } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { BarChart, Bar, XAxis, YAxis, Tooltip, ResponsiveContainer } from "recharts";

export default function CanadianPolitics() {
  const [polls, setPolls] = useState([]);

  useEffect(() => {
    fetch("https://api.example.com/canadian_polls") // Replace with a real API
      .then(response => response.json())
      .then(data => setPolls(data))
      .catch(error => console.error("Error fetching polls:", error));
  }, []);

  return (
    <div className="p-6 space-y-6">
      <h1 className="text-3xl font-bold">Canadian Politics & Polls</h1>
      <p className="text-lg">Stay updated with the latest political polls and learn about Canada’s political system.</p>
      
      <h2 className="text-2xl font-semibold">Latest Polling Data</h2>
      <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
        {polls.map((poll, index) => (
          <Card key={index} className="p-4">
            <CardContent>
              <h3 className="text-xl font-semibold">{poll.title}</h3>
              <p className="text-gray-600">{poll.date}</p>
              <ResponsiveContainer width="100%" height={200}>
                <BarChart data={poll.results}>
                  <XAxis dataKey="party" />
                  <YAxis />
                  <Tooltip />
                  <Bar dataKey="percentage" fill="#8884d8" />
                </BarChart>
              </ResponsiveContainer>
            </CardContent>
          </Card>
        ))}
      </div>
      
      <h2 className="text-2xl font-semibold">Canada’s Political System</h2>
      <p>
        Canada is a parliamentary democracy and constitutional monarchy. The Prime Minister is the head of government,
        while the monarch serves as the head of state. The country is governed through a system of federalism, with
        responsibilities divided between federal and provincial governments.
      </p>
      
      <Button className="mt-4">Learn More</Button>
    </div>
  );
}
