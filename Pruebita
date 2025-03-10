import React, { useState, useEffect } from "react";
import { FiEdit2, FiTrash2, FiPlus, FiSearch, FiX } from "react-icons/fi";

const initialData = [
  {
    id: 1,
    customerName: "John Smith",
    phone: "+1 (555) 123-4567",
    email: "john.smith@email.com",
    vehicleBrand: "Toyota",
    vehicleModel: "Camry",
    vehicleYear: "2020",
    vehiclePlate: "ABC123"
  },
  {
    id: 2,
    customerName: "Emma Johnson",
    phone: "+1 (555) 987-6543",
    email: "emma.j@email.com",
    vehicleBrand: "Honda",
    vehicleModel: "Civic",
    vehicleYear: "2021",
    vehiclePlate: "XYZ789"
  }
];

const WorkshopDashboard = () => {
  const [customers, setCustomers] = useState(initialData);
  const [searchTerm, setSearchTerm] = useState("");
  const [filterType, setFilterType] = useState("name");
  const [isModalOpen, setIsModalOpen] = useState(false);
  const [editingCustomer, setEditingCustomer] = useState(null);
  const [formData, setFormData] = useState({
    customerName: "",
    phone: "",
    email: "",
    vehicleBrand: "",
    vehicleModel: "",
    vehicleYear: "",
    vehiclePlate: ""
  });

  const handleSearch = (value) => {
    setSearchTerm(value);
    const filteredData = initialData.filter(customer => {
      const searchValue = value.toLowerCase();
      switch(filterType) {
        case "name":
          return customer.customerName.toLowerCase().includes(searchValue);
        case "plate":
          return customer.vehiclePlate.toLowerCase().includes(searchValue);
        case "model":
          return customer.vehicleModel.toLowerCase().includes(searchValue);
        default:
          return true;
      }
    });
    setCustomers(filteredData);
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (editingCustomer) {
      setCustomers(customers.map(c => 
        c.id === editingCustomer.id ? { ...formData, id: c.id } : c
      ));
    } else {
      setCustomers([...customers, { ...formData, id: Date.now() }]);
    }
    setIsModalOpen(false);
    setEditingCustomer(null);
    setFormData({
      customerName: "",
      phone: "",
      email: "",
      vehicleBrand: "",
      vehicleModel: "",
      vehicleYear: "",
      vehiclePlate: ""
    });
  };

  const handleEdit = (customer) => {
    setEditingCustomer(customer);
    setFormData(customer);
    setIsModalOpen(true);
  };

  const handleDelete = (id) => {
    if (window.confirm("Are you sure you want to delete this record?")) {
      setCustomers(customers.filter(c => c.id !== id));
    }
  };

  return (
    <div className="min-h-screen bg-[#F5E6D3] p-6 font-['Nunito']">
      <div className="max-w-7xl mx-auto">
        <div className="bg-white rounded-lg shadow-lg p-6">
          <div className="flex flex-col md:flex-row justify-between items-center mb-6">
            <h1 className="text-3xl font-bold text-[#9E2A2B] mb-4 md:mb-0">Workshop Dashboard</h1>
            <button
              onClick={() => setIsModalOpen(true)}
              className="bg-[#FF6B35] text-white px-4 py-2 rounded-lg flex items-center hover:bg-[#F64740] transition-colors"
            >
              <FiPlus className="mr-2" /> Add New Customer
            </button>
          </div>

          <div className="flex flex-col md:flex-row gap-4 mb-6">
            <div className="flex-1 relative">
              <FiSearch className="absolute left-3 top-3 text-gray-400" />
              <input
                type="text"
                placeholder="Search..."
                className="w-full pl-10 pr-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-[#FF6B35]"
                value={searchTerm}
                onChange={(e) => handleSearch(e.target.value)}
              />
            </div>
            <select
              className="p-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-[#FF6B35]"
              value={filterType}
              onChange={(e) => setFilterType(e.target.value)}
            >
              <option value="name">Filter by Name</option>
              <option value="plate">Filter by Plate</option>
              <option value="model">Filter by Model</option>
            </select>
          </div>

          <div className="overflow-x-auto">
            <table className="w-full">
              <thead>
                <tr className="bg-[#FF6B35] text-white">
                  <th className="p-3 text-left">Customer Name</th>
                  <th className="p-3 text-left">Phone</th>
                  <th className="p-3 text-left">Email</th>
                  <th className="p-3 text-left">Vehicle Brand</th>
                  <th className="p-3 text-left">Model</th>
                  <th className="p-3 text-left">Year</th>
                  <th className="p-3 text-left">Plate</th>
                  <th className="p-3 text-left">Actions</th>
                </tr>
              </thead>
              <tbody>
                {customers.map((customer) => (
                  <tr key={customer.id} className="border-b hover:bg-gray-50">
                    <td className="p-3">{customer.customerName}</td>
                    <td className="p-3">{customer.phone}</td>
                    <td className="p-3">{customer.email}</td>
                    <td className="p-3">{customer.vehicleBrand}</td>
                    <td className="p-3">{customer.vehicleModel}</td>
                    <td className="p-3">{customer.vehicleYear}</td>
                    <td className="p-3">{customer.vehiclePlate}</td>
                    <td className="p-3">
                      <div className="flex gap-2">
                        <button
                          onClick={() => handleEdit(customer)}
                          className="p-2 text-blue-600 hover:bg-blue-100 rounded-full"
                          aria-label="Edit"
                        >
                          <FiEdit2 />
                        </button>
                        <button
                          onClick={() => handleDelete(customer.id)}
                          className="p-2 text-red-600 hover:bg-red-100 rounded-full"
                          aria-label="Delete"
                        >
                          <FiTrash2 />
                        </button>
                      </div>
                    </td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        </div>
      </div>

      {isModalOpen && (
        <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4">
          <div className="bg-white rounded-lg p-6 w-full max-w-2xl">
            <div className="flex justify-between items-center mb-6">
              <h2 className="text-2xl font-bold text-[#9E2A2B]">
                {editingCustomer ? "Edit Customer" : "Add New Customer"}
              </h2>
              <button
                onClick={() => {
                  setIsModalOpen(false);
                  setEditingCustomer(null);
                }}
                className="p-2 hover:bg-gray-100 rounded-full"
              >
                <FiX />
              </button>
            </div>
            <form onSubmit={handleSubmit} className="space-y-4">
              <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div>
                  <label className="block mb-1">Customer Name *</label>
                  <input
                    required
                    type="text"
                    value={formData.customerName}
                    onChange={(e) => setFormData({...formData, customerName: e.target.value})}
                    className="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-[#FF6B35]"
                  />
                </div>
                <div>
                  <label className="block mb-1">Phone Number</label>
                  <input
                    type="tel"
                    value={formData.phone}
                    onChange={(e) => setFormData({...formData, phone: e.target.value})}
                    className="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-[#FF6B35]"
                  />
                </div>
                <div>
                  <label className="block mb-1">Email</label>
                  <input
                    type="email"
                    value={formData.email}
                    onChange={(e) => setFormData({...formData, email: e.target.value})}
                    className="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-[#FF6B35]"
                  />
                </div>
                <div>
                  <label className="block mb-1">Vehicle Brand</label>
                  <input
                    type="text"
                    value={formData.vehicleBrand}
                    onChange={(e) => setFormData({...formData, vehicleBrand: e.target.value})}
                    className="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-[#FF6B35]"
                  />
                </div>
                <div>
                  <label className="block mb-1">Vehicle Model</label>
                  <input
                    type="text"
                    value={formData.vehicleModel}
                    onChange={(e) => setFormData({...formData, vehicleModel: e.target.value})}
                    className="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-[#FF6B35]"
                  />
                </div>
                <div>
                  <label className="block mb-1">Vehicle Year</label>
                  <input
                    type="text"
                    value={formData.vehicleYear}
                    onChange={(e) => setFormData({...formData, vehicleYear: e.target.value})}
                    className="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-[#FF6B35]"
                  />
                </div>
                <div>
                  <label className="block mb-1">Vehicle Plate</label>
                  <input
                    type="text"
                    value={formData.vehiclePlate}
                    onChange={(e) => setFormData({...formData, vehiclePlate: e.target.value})}
                    className="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-[#FF6B35]"
                  />
                </div>
              </div>
              <div className="flex justify-end gap-4 mt-6">
                <button
                  type="button"
                  onClick={() => {
                    setIsModalOpen(false);
                    setEditingCustomer(null);
                  }}
                  className="px-4 py-2 border rounded-lg hover:bg-gray-100"
                >
                  Cancel
                </button>
                <button
                  type="submit"
                  className="px-4 py-2 bg-[#FF6B35] text-white rounded-lg hover:bg-[#F64740] transition-colors"
                >
                  {editingCustomer ? "Update" : "Save"}
                </button>
              </div>
            </form>
          </div>
        </div>
      )}
    </div>
  );
};

export default WorkshopDashboard;
