# project-5
sing System;
using System.Linq;
using System.IO;
using System.Text;
using System.Collections;
using System.Collections.Generic;

class Player
{
    static void Main(string[] args){
        string[] inputs;
        inputs = Console.ReadLine().Split(' ');
        int N = int.Parse(inputs[0]);
        int L = int.Parse(inputs[1]);
        int E = int.Parse(inputs[2]);

        List<Link> links = new List<Link>();
        for (int i = 0; i < L; i++){
            inputs = Console.ReadLine().Split(' ');
            links.Add(new Link(int.Parse(inputs[0]), int.Parse(inputs[1])));
        }
        List<int> gateways = new List<int>();
        for (int i = 0; i < E; i++)
            gateways.Add(int.Parse(Console.ReadLine()));


            while (true){
                int SI = int.Parse(Console.ReadLine());

                Link.CloseGateway(SI, gateways, links);
            }
    }
}

public class Link{
    public int p { get; set; }
    public int t { get; set; }

    public Link(int node1, int node2){
        p = node1;
        t = node2;
    }
    public override string ToString(){ return $"{p} {t}"; }

    public override bool Equals(object obj){
        Link link = obj as Link;
        return (p == link.p && t == link.t) || (p == link.t && t == link.p);
    }
            static public void CloseGateway(int agentIndex, List<int> gateways, List<Link> links){
                foreach (int gateway in gateways){
                    Link link = new Link(agentIndex, gateway);
                    if (links.Contains(link)){
                        Console.WriteLine(link);
                        links.Remove(link);
                        return;
                    }
                }
                Console.WriteLine(links[new Random().Next(0, links.Count)]);
    }
}
