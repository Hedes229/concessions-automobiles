// The exported code uses Tailwind CSS. Install Tailwind CSS in your dev environment to ensure all styles work.

import React, { useState, useEffect } from "react";

const App: React.FC = () => {
  const [sortOption, setSortOption] = useState("popularity");
  const [viewMode, setViewMode] = useState("grid");
  const [priceRange, setPriceRange] = useState([100000, 5000000]);
  const [yearRange, setYearRange] = useState([2020, 2025]);
  const [selectedBrands, setSelectedBrands] = useState<string[]>([]);
  const [selectedBodyTypes, setSelectedBodyTypes] = useState<string[]>([]);
  const [isMenuOpen, setIsMenuOpen] = useState(false);
  const [isFilterOpen, setIsFilterOpen] = useState(false);

  const brands = [
    { id: "lamborghini", name: "Lamborghini" },
    { id: "ferrari", name: "Ferrari" },
    { id: "porsche", name: "Porsche" },
    { id: "rolls-royce", name: "Rolls-Royce" },
    { id: "bentley", name: "Bentley" },
    { id: "aston-martin", name: "Aston Martin" },
    { id: "bugatti", name: "Bugatti" },
    { id: "mclaren", name: "McLaren" },
  ];

  const bodyTypes = [
    { id: "coupe", name: "Coupe" },
    { id: "convertible", name: "Convertible" },
    { id: "sedan", name: "Sedan" },
    { id: "suv", name: "SUV" },
    { id: "hypercar", name: "Hypercar" },
  ];

  const vehicles = [
    {
      id: 1,
      name: "Lamborghini Aventador",
      brand: "Lamborghini",
      year: 2025,
      price: 450000,
      bodyType: "coupe",
      specs: {
        power: "770 HP",
        acceleration: "2.8s",
        topSpeed: "220 mph",
      },
      imageUrl:
        "https://readdy.ai/api/search-image?query=Lamborghini%2520Aventador%2520in%2520matte%2520black%2520color%2520against%2520minimalist%2520luxury%2520showroom%2520background%2520with%2520soft%2520lighting%2520highlighting%2520the%2520aerodynamic%2520design%2520and%2520angular%2520features%2520professional%2520automotive%2520photography%2520with%2520dramatic%2520shadows%2520and%2520reflections%2520sophisticated%2520atmosphere&width=600&height=400&seq=101&orientation=landscape",
    },
    {
      id: 2,
      name: "Ferrari SF90 Stradale",
      brand: "Ferrari",
      year: 2025,
      price: 520000,
      bodyType: "coupe",
      specs: {
        power: "986 HP",
        acceleration: "2.5s",
        topSpeed: "211 mph",
      },
      imageUrl:
        "https://readdy.ai/api/search-image?query=Ferrari%2520SF90%2520Stradale%2520in%2520vibrant%2520red%2520color%2520against%2520minimalist%2520luxury%2520showroom%2520background%2520with%2520soft%2520lighting%2520highlighting%2520the%2520aerodynamic%2520design%2520and%2520sleek%2520curves%2520professional%2520automotive%2520photography%2520with%2520dramatic%2520shadows%2520and%2520reflections%2520sophisticated%2520atmosphere&width=600&height=400&seq=102&orientation=landscape",
    },
    {
      id: 3,
      name: "Porsche 911 GT3 RS",
      brand: "Porsche",
      year: 2025,
      price: 220000,
      bodyType: "coupe",
      specs: {
        power: "518 HP",
        acceleration: "3.2s",
        topSpeed: "184 mph",
      },
      imageUrl:
        "https://readdy.ai/api/search-image?query=Porsche%2520911%2520GT3%2520RS%2520in%2520silver%2520metallic%2520color%2520against%2520minimalist%2520luxury%2520showroom%2520background%2520with%2520soft%2520lighting%2520highlighting%2520the%2520aerodynamic%2520design%2520and%2520racing%2520features%2520professional%2520automotive%2520photography%2520with%2520dramatic%2520shadows%2520and%2520reflections%2520sophisticated%2520atmosphere&width=600&height=400&seq=103&orientation=landscape",
    },
    {
      id: 4,
      name: "Rolls-Royce Phantom",
      brand: "Rolls-Royce",
      year: 2025,
      price: 455000,
      bodyType: "sedan",
      specs: {
        power: "563 HP",
        acceleration: "5.1s",
        topSpeed: "155 mph",
      },
      imageUrl:
        "https://readdy.ai/api/search-image?query=Rolls%2520Royce%2520Phantom%2520in%2520elegant%2520black%2520color%2520against%2520minimalist%2520luxury%2520showroom%2520background%2520with%2520soft%2520lighting%2520highlighting%2520the%2520prestigious%2520design%2520and%2520luxurious%2520features%2520professional%2520automotive%2520photography%2520with%2520dramatic%2520shadows%2520and%2520reflections%2520sophisticated%2520atmosphere&width=600&height=400&seq=104&orientation=landscape",
    },
    {
      id: 5,
      name: "Bentley Continental GT",
      brand: "Bentley",
      year: 2025,
      price: 235000,
      bodyType: "coupe",
      specs: {
        power: "650 HP",
        acceleration: "3.5s",
        topSpeed: "208 mph",
      },
      imageUrl:
        "https://readdy.ai/api/search-image?query=Bentley%2520Continental%2520GT%2520in%2520British%2520racing%2520green%2520color%2520against%2520minimalist%2520luxury%2520showroom%2520background%2520with%2520soft%2520lighting%2520highlighting%2520the%2520elegant%2520design%2520and%2520luxurious%2520features%2520professional%2520automotive%2520photography%2520with%2520dramatic%2520shadows%2520and%2520reflections%2520sophisticated%2520atmosphere&width=600&height=400&seq=105&orientation=landscape",
    },
    {
      id: 6,
      name: "Aston Martin DBS",
      brand: "Aston Martin",
      year: 2025,
      price: 330000,
      bodyType: "coupe",
      specs: {
        power: "715 HP",
        acceleration: "3.4s",
        topSpeed: "211 mph",
      },
      imageUrl:
        "https://readdy.ai/api/search-image?query=Aston%2520Martin%2520DBS%2520in%2520silver%2520color%2520against%2520minimalist%2520luxury%2520showroom%2520background%2520with%2520soft%2520lighting%2520highlighting%2520the%2520elegant%2520design%2520and%2520sporty%2520features%2520professional%2520automotive%2520photography%2520with%2520dramatic%2520shadows%2520and%2520reflections%2520sophisticated%2520atmosphere&width=600&height=400&seq=106&orientation=landscape",
    },
    {
      id: 7,
      name: "McLaren 720S",
      brand: "McLaren",
      year: 2025,
      price: 310000,
      bodyType: "coupe",
      specs: {
        power: "710 HP",
        acceleration: "2.8s",
        topSpeed: "212 mph",
      },
      imageUrl:
        "https://readdy.ai/api/search-image?query=McLaren%2520720S%2520in%2520papaya%2520orange%2520color%2520against%2520minimalist%2520luxury%2520showroom%2520background%2520with%2520soft%2520lighting%2520highlighting%2520the%2520futuristic%2520design%2520and%2520aerodynamic%2520features%2520professional%2520automotive%2520photography%2520with%2520dramatic%2520shadows%2520and%2520reflections%2520sophisticated%2520atmosphere&width=600&height=400&seq=107&orientation=landscape",
    },
    {
      id: 8,
      name: "Bugatti Chiron",
      brand: "Bugatti",
      year: 2025,
      price: 3200000,
      bodyType: "hypercar",
      specs: {
        power: "1500 HP",
        acceleration: "2.4s",
        topSpeed: "261 mph",
      },
      imageUrl:
        "https://readdy.ai/api/search-image?query=Bugatti%2520Chiron%2520in%2520royal%2520blue%2520and%2520black%2520two%2520tone%2520color%2520against%2520minimalist%2520luxury%2520showroom%2520background%2520with%2520soft%2520lighting%2520highlighting%2520the%2520hypercar%2520design%2520and%2520engineering%2520excellence%2520professional%2520automotive%2520photography%2520with%2520dramatic%2520shadows%2520and%2520reflections%2520sophisticated%2520atmosphere&width=600&height=400&seq=108&orientation=landscape",
    },
    {
      id: 9,
      name: "Lamborghini Urus",
      brand: "Lamborghini",
      year: 2025,
      price: 230000,
      bodyType: "suv",
      specs: {
        power: "650 HP",
        acceleration: "3.6s",
        topSpeed: "190 mph",
      },
      imageUrl:
        "https://readdy.ai/api/search-image?query=Lamborghini%2520Urus%2520in%2520yellow%2520color%2520against%2520minimalist%2520luxury%2520showroom%2520background%2520with%2520soft%2520lighting%2520highlighting%2520the%2520aggressive%2520SUV%2520design%2520and%2520sporty%2520features%2520professional%2520automotive%2520photography%2520with%2520dramatic%2520shadows%2520and%2520reflections%2520sophisticated%2520atmosphere&width=600&height=400&seq=109&orientation=landscape",
    },
    {
      id: 10,
      name: "Ferrari Roma",
      brand: "Ferrari",
      year: 2025,
      price: 250000,
      bodyType: "coupe",
      specs: {
        power: "612 HP",
        acceleration: "3.4s",
        topSpeed: "199 mph",
      },
      imageUrl:
        "https://readdy.ai/api/search-image?query=Ferrari%2520Roma%2520in%2520silver%2520blue%2520color%2520against%2520minimalist%2520luxury%2520showroom%2520background%2520with%2520soft%2520lighting%2520highlighting%2520the%2520elegant%2520design%2520and%2520timeless%2520features%2520professional%2520automotive%2520photography%2520with%2520dramatic%2520shadows%2520and%2520reflections%2520sophisticated%2520atmosphere&width=600&height=400&seq=110&orientation=landscape",
    },
    {
      id: 11,
      name: "Porsche Taycan Turbo S",
      brand: "Porsche",
      year: 2025,
      price: 190000,
      bodyType: "sedan",
      specs: {
        power: "750 HP",
        acceleration: "2.6s",
        topSpeed: "161 mph",
      },
      imageUrl:
        "https://readdy.ai/api/search-image?query=Porsche%2520Taycan%2520Turbo%2520S%2520in%2520white%2520color%2520against%2520minimalist%2520luxury%2520showroom%2520background%2520with%2520soft%2520lighting%2520highlighting%2520the%2520electric%2520sedan%2520design%2520and%2520futuristic%2520features%2520professional%2520automotive%2520photography%2520with%2520dramatic%2520shadows%2520and%2520reflections%2520sophisticated%2520atmosphere&width=600&height=400&seq=111&orientation=landscape",
    },
    {
      id: 12,
      name: "Bentley Bentayga",
      brand: "Bentley",
      year: 2025,
      price: 245000,
      bodyType: "suv",
      specs: {
        power: "626 HP",
        acceleration: "3.8s",
        topSpeed: "180 mph",
      },
      imageUrl:
        "https://readdy.ai/api/search-image?query=Bentley%2520Bentayga%2520in%2520dark%2520burgundy%2520color%2520against%2520minimalist%2520luxury%2520showroom%2520background%2520with%2520soft%2520lighting%2520highlighting%2520the%2520luxury%2520SUV%2520design%2520and%2520premium%2520features%2520professional%2520automotive%2520photography%2520with%2520dramatic%2520shadows%2520and%2520reflections%2520sophisticated%2520atmosphere&width=600&height=400&seq=112&orientation=landscape",
    },
  ];

  const toggleMenu = () => {
    setIsMenuOpen(!isMenuOpen);
  };

  const toggleFilter = () => {
    setIsFilterOpen(!isFilterOpen);
  };

  const handleBrandChange = (brandId: string) => {
    if (selectedBrands.includes(brandId)) {
      setSelectedBrands(selectedBrands.filter((id) => id !== brandId));
    } else {
      setSelectedBrands([...selectedBrands, brandId]);
    }
  };

  const handleBodyTypeChange = (bodyTypeId: string) => {
    if (selectedBodyTypes.includes(bodyTypeId)) {
      setSelectedBodyTypes(selectedBodyTypes.filter((id) => id !== bodyTypeId));
    } else {
      setSelectedBodyTypes([...selectedBodyTypes, bodyTypeId]);
    }
  };

  const clearAllFilters = () => {
    setSelectedBrands([]);
    setSelectedBodyTypes([]);
    setPriceRange([100000, 5000000]);
    setYearRange([2020, 2025]);
    setSortOption("popularity");
  };

  const formatPrice = (price: number) => {
    return `$${price.toLocaleString()}`;
  };

  const filteredVehicles = vehicles.filter((vehicle) => {
    const matchesBrand =
      selectedBrands.length === 0 ||
      selectedBrands.includes(vehicle.brand.toLowerCase());
    const matchesBodyType =
      selectedBodyTypes.length === 0 ||
      selectedBodyTypes.includes(vehicle.bodyType);
    const matchesPriceRange =
      vehicle.price >= priceRange[0] && vehicle.price <= priceRange[1];
    const matchesYearRange =
      vehicle.year >= yearRange[0] && vehicle.year <= yearRange[1];

    return (
      matchesBrand && matchesBodyType && matchesPriceRange && matchesYearRange
    );
  });

  const sortedVehicles = [...filteredVehicles].sort((a, b) => {
    if (sortOption === "price-low") {
      return a.price - b.price;
    } else if (sortOption === "price-high") {
      return b.price - a.price;
    } else if (sortOption === "newest") {
      return b.year - a.year;
    }
    // Default: popularity (by id)
    return a.id - b.id;
  });

  return (
    <div className="min-h-screen font-sans bg-white text-gray-900">
      {/* Header */}
      <header className="fixed top-0 left-0 right-0 z-50 bg-black/90">
        <div className="container mx-auto px-6 py-4">
          <div className="flex items-center justify-between">
            <div className="flex items-center">
              <h1 className="text-2xl font-bold text-white mr-2">LUXE</h1>
              <span className="text-amber-500 text-2xl font-light">MOTORS</span>
            </div>
            <div className="hidden md:flex items-center space-x-8">
              <a
                href="https://readdy.ai/home/68fc91bc-34e7-47cc-8779-b3ad9976abda/8548099c-0e99-4419-8cfd-41bd85bb7724"
                data-readdy="true"
                className="text-white hover:text-amber-500 transition-colors duration-300"
              >
                Home
              </a>
              <a
                href="#inventory"
                className="text-amber-500 border-b-2 border-amber-500 pb-1"
              >
                Inventory
              </a>
              <a
                href="#about"
                className="text-white hover:text-amber-500 transition-colors duration-300"
              >
                About Us
              </a>
              <a
                href="#testimonials"
                className="text-white hover:text-amber-500 transition-colors duration-300"
              >
                Testimonials
              </a>
              <a
                href="#contact"
                className="text-white hover:text-amber-500 transition-colors duration-300"
              >
                Contact
              </a>
              <button className="bg-gradient-to-r from-amber-600 to-amber-500 text-white px-6 py-2 !rounded-button whitespace-nowrap cursor-pointer hover:from-amber-500 hover:to-amber-400 transition-all duration-300">
                Book a Test Drive
              </button>
            </div>
            <div className="md:hidden">
              <button
                onClick={toggleMenu}
                className="text-white cursor-pointer"
              >
                <i
                  className={`fas ${isMenuOpen ? "fa-times" : "fa-bars"} text-2xl`}
                ></i>
              </button>
            </div>
          </div>
        </div>
        {/* Mobile Menu */}
        {isMenuOpen && (
          <div className="md:hidden bg-black/95 py-4">
            <div className="container mx-auto px-6 flex flex-col space-y-4">
              <a
                href="https://readdy.ai/home/68fc91bc-34e7-47cc-8779-b3ad9976abda/8548099c-0e99-4419-8cfd-41bd85bb7724"
                data-readdy="true"
                className="text-white hover:text-amber-500 transition-colors duration-300 py-2"
              >
                Home
              </a>
              <a href="#inventory" className="text-amber-500 py-2">
                Inventory
              </a>
              <a
                href="#about"
                className="text-white hover:text-amber-500 transition-colors duration-300 py-2"
              >
                About Us
              </a>
              <a
                href="#testimonials"
                className="text-white hover:text-amber-500 transition-colors duration-300 py-2"
              >
                Testimonials
              </a>
              <a
                href="#contact"
                className="text-white hover:text-amber-500 transition-colors duration-300 py-2"
              >
                Contact
              </a>
              <button className="bg-gradient-to-r from-amber-600 to-amber-500 text-white px-6 py-3 !rounded-button whitespace-nowrap cursor-pointer hover:from-amber-500 hover:to-amber-400 transition-all duration-300">
                Book a Test Drive
              </button>
            </div>
          </div>
        )}
      </header>

      {/* Collection Header */}
      <section className="pt-32 pb-12 bg-gray-50">
        <div className="container mx-auto px-6">
          <div className="text-center mb-12">
            <h1 className="text-5xl font-bold mb-4">Our Collection</h1>
            <p className="text-gray-600 max-w-3xl mx-auto">
              Discover our handpicked selection of the world's most exclusive
              automobiles, each representing the pinnacle of engineering
              excellence, design innovation, and luxury craftsmanship.
            </p>
          </div>

          {/* Filtering Toolbar */}
          <div className="flex flex-col md:flex-row justify-between items-center bg-white p-4 rounded-lg shadow mb-8">
            <div className="flex items-center mb-4 md:mb-0">
              <span className="text-gray-700 mr-3">Sort by:</span>
              <div className="relative">
                <select
                  value={sortOption}
                  onChange={(e) => setSortOption(e.target.value)}
                  className="appearance-none bg-gray-50 border border-gray-200 rounded-lg px-4 py-2 pr-8 focus:outline-none focus:ring-2 focus:ring-amber-500 cursor-pointer"
                >
                  <option value="popularity">Popularity</option>
                  <option value="price-low">Price: Low to High</option>
                  <option value="price-high">Price: High to Low</option>
                  <option value="newest">Newest</option>
                </select>
                <div className="absolute right-3 top-1/2 transform -translate-y-1/2 pointer-events-none">
                  <i className="fas fa-chevron-down text-gray-400"></i>
                </div>
              </div>
            </div>

            <div className="flex items-center">
              <span className="text-gray-700 mr-3 hidden md:inline">View:</span>
              <div className="flex border border-gray-200 rounded-lg overflow-hidden">
                <button
                  onClick={() => setViewMode("grid")}
                  className={`px-3 py-2 ${viewMode === "grid" ? "bg-amber-500 text-white" : "bg-gray-50 text-gray-700"}`}
                >
                  <i className="fas fa-th-large"></i>
                </button>
                <button
                  onClick={() => setViewMode("list")}
                  className={`px-3 py-2 ${viewMode === "list" ? "bg-amber-500 text-white" : "bg-gray-50 text-gray-700"}`}
                >
                  <i className="fas fa-list"></i>
                </button>
              </div>
              <button
                onClick={toggleFilter}
                className="ml-4 px-4 py-2 bg-gray-800 text-white rounded-lg md:hidden"
              >
                <i className="fas fa-filter mr-2"></i> Filters
              </button>
            </div>
          </div>
        </div>
      </section>

      {/* Main Content with Sidebar */}
      <section className="py-8 bg-white">
        <div className="container mx-auto px-6">
          <div className="flex flex-col md:flex-row">
            {/* Filter Sidebar - Desktop */}
            <div className="hidden md:block w-64 mr-8">
              <div className="bg-gray-50 rounded-lg shadow p-6 sticky top-24">
                <div className="flex justify-between items-center mb-6">
                  <h3 className="text-xl font-bold">Filters</h3>
                  <button
                    onClick={clearAllFilters}
                    className="text-amber-600 hover:text-amber-700 text-sm font-medium cursor-pointer"
                  >
                    Clear All
                  </button>
                </div>

                {/* Brand Filter */}
                <div className="mb-8">
                  <h4 className="font-bold mb-3 text-gray-800">Brand</h4>
                  <div className="space-y-2">
                    {brands.map((brand) => (
                      <div key={brand.id} className="flex items-center">
                        <input
                          type="checkbox"
                          id={`brand-${brand.id}`}
                          checked={selectedBrands.includes(brand.id)}
                          onChange={() => handleBrandChange(brand.id)}
                          className="w-4 h-4 text-amber-600 border-gray-300 rounded focus:ring-amber-500"
                        />
                        <label
                          htmlFor={`brand-${brand.id}`}
                          className="ml-2 text-gray-700 cursor-pointer"
                        >
                          {brand.name}
                        </label>
                      </div>
                    ))}
                  </div>
                </div>

                {/* Price Range */}
                <div className="mb-8">
                  <h4 className="font-bold mb-3 text-gray-800">Price Range</h4>
                  <div className="px-2">
                    <input
                      type="range"
                      min="100000"
                      max="5000000"
                      step="50000"
                      value={priceRange[1]}
                      onChange={(e) =>
                        setPriceRange([priceRange[0], parseInt(e.target.value)])
                      }
                      className="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer accent-amber-500"
                    />
                    <div className="flex justify-between mt-2 text-sm text-gray-600">
                      <span>{formatPrice(priceRange[0])}</span>
                      <span>{formatPrice(priceRange[1])}</span>
                    </div>
                  </div>
                </div>

                {/* Body Type */}
                <div className="mb-8">
                  <h4 className="font-bold mb-3 text-gray-800">Body Type</h4>
                  <div className="space-y-2">
                    {bodyTypes.map((bodyType) => (
                      <div key={bodyType.id} className="flex items-center">
                        <input
                          type="checkbox"
                          id={`bodyType-${bodyType.id}`}
                          checked={selectedBodyTypes.includes(bodyType.id)}
                          onChange={() => handleBodyTypeChange(bodyType.id)}
                          className="w-4 h-4 text-amber-600 border-gray-300 rounded focus:ring-amber-500"
                        />
                        <label
                          htmlFor={`bodyType-${bodyType.id}`}
                          className="ml-2 text-gray-700 cursor-pointer"
                        >
                          {bodyType.name}
                        </label>
                      </div>
                    ))}
                  </div>
                </div>

                {/* Year Range */}
                <div className="mb-6">
                  <h4 className="font-bold mb-3 text-gray-800">Year</h4>
                  <div className="px-2">
                    <div className="flex justify-between mb-2">
                      <input
                        type="number"
                        min="2020"
                        max="2025"
                        value={yearRange[0]}
                        onChange={(e) =>
                          setYearRange([parseInt(e.target.value), yearRange[1]])
                        }
                        className="w-24 px-2 py-1 border border-gray-300 rounded text-center"
                      />
                      <span className="mx-2 self-center">-</span>
                      <input
                        type="number"
                        min="2020"
                        max="2025"
                        value={yearRange[1]}
                        onChange={(e) =>
                          setYearRange([yearRange[0], parseInt(e.target.value)])
                        }
                        className="w-24 px-2 py-1 border border-gray-300 rounded text-center"
                      />
                    </div>
                    <input
                      type="range"
                      min="2020"
                      max="2025"
                      step="1"
                      value={yearRange[1]}
                      onChange={(e) =>
                        setYearRange([yearRange[0], parseInt(e.target.value)])
                      }
                      className="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer accent-amber-500"
                    />
                  </div>
                </div>
              </div>
            </div>

            {/* Filter Sidebar - Mobile */}
            {isFilterOpen && (
              <div className="fixed inset-0 bg-black bg-opacity-50 z-50 md:hidden">
                <div className="absolute right-0 top-0 bottom-0 w-80 bg-white shadow-xl overflow-y-auto">
                  <div className="p-6">
                    <div className="flex justify-between items-center mb-6">
                      <h3 className="text-xl font-bold">Filters</h3>
                      <button
                        onClick={toggleFilter}
                        className="text-gray-500 hover:text-gray-700"
                      >
                        <i className="fas fa-times text-xl"></i>
                      </button>
                    </div>

                    {/* Brand Filter */}
                    <div className="mb-8">
                      <h4 className="font-bold mb-3 text-gray-800">Brand</h4>
                      <div className="space-y-2">
                        {brands.map((brand) => (
                          <div key={brand.id} className="flex items-center">
                            <input
                              type="checkbox"
                              id={`mobile-brand-${brand.id}`}
                              checked={selectedBrands.includes(brand.id)}
                              onChange={() => handleBrandChange(brand.id)}
                              className="w-4 h-4 text-amber-600 border-gray-300 rounded focus:ring-amber-500"
                            />
                            <label
                              htmlFor={`mobile-brand-${brand.id}`}
                              className="ml-2 text-gray-700 cursor-pointer"
                            >
                              {brand.name}
                            </label>
                          </div>
                        ))}
                      </div>
                    </div>

                    {/* Price Range */}
                    <div className="mb-8">
                      <h4 className="font-bold mb-3 text-gray-800">
                        Price Range
                      </h4>
                      <div className="px-2">
                        <input
                          type="range"
                          min="100000"
                          max="5000000"
                          step="50000"
                          value={priceRange[1]}
                          onChange={(e) =>
                            setPriceRange([
                              priceRange[0],
                              parseInt(e.target.value),
                            ])
                          }
                          className="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer accent-amber-500"
                        />
                        <div className="flex justify-between mt-2 text-sm text-gray-600">
                          <span>{formatPrice(priceRange[0])}</span>
                          <span>{formatPrice(priceRange[1])}</span>
                        </div>
                      </div>
                    </div>

                    {/* Body Type */}
                    <div className="mb-8">
                      <h4 className="font-bold mb-3 text-gray-800">
                        Body Type
                      </h4>
                      <div className="space-y-2">
                        {bodyTypes.map((bodyType) => (
                          <div key={bodyType.id} className="flex items-center">
                            <input
                              type="checkbox"
                              id={`mobile-bodyType-${bodyType.id}`}
                              checked={selectedBodyTypes.includes(bodyType.id)}
                              onChange={() => handleBodyTypeChange(bodyType.id)}
                              className="w-4 h-4 text-amber-600 border-gray-300 rounded focus:ring-amber-500"
                            />
                            <label
                              htmlFor={`mobile-bodyType-${bodyType.id}`}
                              className="ml-2 text-gray-700 cursor-pointer"
                            >
                              {bodyType.name}
                            </label>
                          </div>
                        ))}
                      </div>
                    </div>

                    {/* Year Range */}
                    <div className="mb-8">
                      <h4 className="font-bold mb-3 text-gray-800">Year</h4>
                      <div className="px-2">
                        <div className="flex justify-between mb-2">
                          <input
                            type="number"
                            min="2020"
                            max="2025"
                            value={yearRange[0]}
                            onChange={(e) =>
                              setYearRange([
                                parseInt(e.target.value),
                                yearRange[1],
                              ])
                            }
                            className="w-24 px-2 py-1 border border-gray-300 rounded text-center"
                          />
                          <span className="mx-2 self-center">-</span>
                          <input
                            type="number"
                            min="2020"
                            max="2025"
                            value={yearRange[1]}
                            onChange={(e) =>
                              setYearRange([
                                yearRange[0],
                                parseInt(e.target.value),
                              ])
                            }
                            className="w-24 px-2 py-1 border border-gray-300 rounded text-center"
                          />
                        </div>
                        <input
                          type="range"
                          min="2020"
                          max="2025"
                          step="1"
                          value={yearRange[1]}
                          onChange={(e) =>
                            setYearRange([
                              yearRange[0],
                              parseInt(e.target.value),
                            ])
                          }
                          className="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer accent-amber-500"
                        />
                      </div>
                    </div>

                    <div className="flex space-x-4">
                      <button
                        onClick={clearAllFilters}
                        className="flex-1 py-3 border border-gray-300 rounded-lg text-gray-700 font-medium hover:bg-gray-50 !rounded-button whitespace-nowrap cursor-pointer"
                      >
                        Clear All
                      </button>
                      <button
                        onClick={toggleFilter}
                        className="flex-1 py-3 bg-amber-500 text-white rounded-lg font-medium hover:bg-amber-600 !rounded-button whitespace-nowrap cursor-pointer"
                      >
                        Apply Filters
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            )}

            {/* Vehicle Grid */}
            <div className="flex-1">
              {sortedVehicles.length > 0 ? (
                <div
                  className={
                    viewMode === "grid"
                      ? "grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8"
                      : "space-y-6"
                  }
                >
                  {sortedVehicles.map((vehicle) =>
                    viewMode === "grid" ? (
                      <div
                        key={vehicle.id}
                        className="bg-white rounded-lg overflow-hidden shadow-lg hover:shadow-2xl transition-shadow duration-300 group"
                      >
                        <div className="relative overflow-hidden h-48">
                          <img
                            src={vehicle.imageUrl}
                            alt={vehicle.name}
                            className="w-full h-full object-cover object-center group-hover:scale-105 transition-transform duration-500"
                          />
                          <div className="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end">
                            <div className="p-4 w-full">
                              <div className="grid grid-cols-3 gap-2 text-white text-sm mb-3">
                                <div className="text-center">
                                  <div className="font-bold">
                                    {vehicle.specs.power}
                                  </div>
                                  <div className="text-xs text-gray-300">
                                    Power
                                  </div>
                                </div>
                                <div className="text-center">
                                  <div className="font-bold">
                                    {vehicle.specs.acceleration}
                                  </div>
                                  <div className="text-xs text-gray-300">
                                    0-60 mph
                                  </div>
                                </div>
                                <div className="text-center">
                                  <div className="font-bold">
                                    {vehicle.specs.topSpeed}
                                  </div>
                                  <div className="text-xs text-gray-300">
                                    Top Speed
                                  </div>
                                </div>
                              </div>
                              <button className="bg-white text-gray-900 w-full py-2 !rounded-button whitespace-nowrap cursor-pointer hover:bg-amber-500 hover:text-white transition-all duration-300">
                                View Details
                              </button>
                            </div>
                          </div>
                        </div>
                        <div className="p-5">
                          <div className="flex justify-between items-start mb-2">
                            <h3 className="text-lg font-bold">
                              {vehicle.name}
                            </h3>
                            <span className="text-amber-600 font-semibold">
                              {formatPrice(vehicle.price)}
                            </span>
                          </div>
                          <div className="flex justify-between items-center text-gray-600 text-sm">
                            <span>{vehicle.brand}</span>
                            <span>{vehicle.year}</span>
                          </div>
                        </div>
                      </div>
                    ) : (
                      <div
                        key={vehicle.id}
                        className="bg-white rounded-lg overflow-hidden shadow-lg hover:shadow-xl transition-shadow duration-300 flex flex-col md:flex-row"
                      >
                        <div className="md:w-1/3 relative overflow-hidden h-48 md:h-auto">
                          <img
                            src={vehicle.imageUrl}
                            alt={vehicle.name}
                            className="w-full h-full object-cover object-center hover:scale-105 transition-transform duration-500"
                          />
                        </div>
                        <div className="md:w-2/3 p-6 flex flex-col">
                          <div className="flex justify-between items-start mb-3">
                            <div>
                              <h3 className="text-xl font-bold mb-1">
                                {vehicle.name}
                              </h3>
                              <div className="text-gray-600 text-sm">
                                {vehicle.brand} | {vehicle.year} |{" "}
                                {vehicle.bodyType.charAt(0).toUpperCase() +
                                  vehicle.bodyType.slice(1)}
                              </div>
                            </div>
                            <span className="text-amber-600 font-semibold text-xl">
                              {formatPrice(vehicle.price)}
                            </span>
                          </div>

                          <div className="grid grid-cols-3 gap-4 my-4">
                            <div className="text-center p-2 bg-gray-50 rounded">
                              <div className="font-bold">
                                {vehicle.specs.power}
                              </div>
                              <div className="text-xs text-gray-500">Power</div>
                            </div>
                            <div className="text-center p-2 bg-gray-50 rounded">
                              <div className="font-bold">
                                {vehicle.specs.acceleration}
                              </div>
                              <div className="text-xs text-gray-500">
                                0-60 mph
                              </div>
                            </div>
                            <div className="text-center p-2 bg-gray-50 rounded">
                              <div className="font-bold">
                                {vehicle.specs.topSpeed}
                              </div>
                              <div className="text-xs text-gray-500">
                                Top Speed
                              </div>
                            </div>
                          </div>

                          <div className="mt-auto">
                            <button className="bg-gradient-to-r from-amber-600 to-amber-500 text-white px-6 py-2 !rounded-button whitespace-nowrap cursor-pointer hover:from-amber-500 hover:to-amber-400 transition-all duration-300">
                              View Details
                            </button>
                          </div>
                        </div>
                      </div>
                    ),
                  )}
                </div>
              ) : (
                <div className="bg-white rounded-lg shadow-lg p-12 text-center">
                  <div className="text-amber-500 mb-4">
                    <i className="fas fa-search text-6xl"></i>
                  </div>
                  <h3 className="text-2xl font-bold mb-4">No vehicles found</h3>
                  <p className="text-gray-600 mb-6">
                    We couldn't find any vehicles matching your current filters.
                    Try adjusting your search criteria.
                  </p>
                  <button
                    onClick={clearAllFilters}
                    className="bg-gradient-to-r from-amber-600 to-amber-500 text-white px-8 py-3 !rounded-button whitespace-nowrap cursor-pointer hover:from-amber-500 hover:to-amber-400 transition-all duration-300"
                  >
                    Clear All Filters
                  </button>
                </div>
              )}

              {/* Pagination */}
              {sortedVehicles.length > 0 && (
                <div className="mt-12 flex justify-center">
                  <div className="flex space-x-2">
                    <button className="w-10 h-10 rounded-full bg-amber-500 text-white flex items-center justify-center cursor-pointer">
                      1
                    </button>
                    <button className="w-10 h-10 rounded-full bg-gray-200 text-gray-700 flex items-center justify-center hover:bg-gray-300 cursor-pointer">
                      2
                    </button>
                    <button className="w-10 h-10 rounded-full bg-gray-200 text-gray-700 flex items-center justify-center hover:bg-gray-300 cursor-pointer">
                      3
                    </button>
                    <button className="w-10 h-10 rounded-full bg-gray-200 text-gray-700 flex items-center justify-center hover:bg-gray-300 cursor-pointer">
                      <i className="fas fa-ellipsis-h"></i>
                    </button>
                  </div>
                </div>
              )}
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-gray-900 text-white pt-16 pb-8 mt-16">
        <div className="container mx-auto px-6">
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-12 mb-16">
            <div>
              <div className="flex items-center mb-6">
                <h1 className="text-2xl font-bold text-white mr-2">LUXE</h1>
                <span className="text-amber-500 text-2xl font-light">
                  MOTORS
                </span>
              </div>
              <p className="text-gray-400 mb-6">
                The premier destination for luxury and exotic automobiles,
                offering an unparalleled selection of the world's finest
                vehicles.
              </p>
              <div className="flex space-x-4">
                <a
                  href="#"
                  className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                >
                  <i className="fab fa-facebook-f text-xl"></i>
                </a>
                <a
                  href="#"
                  className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                >
                  <i className="fab fa-instagram text-xl"></i>
                </a>
                <a
                  href="#"
                  className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                >
                  <i className="fab fa-twitter text-xl"></i>
                </a>
                <a
                  href="#"
                  className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                >
                  <i className="fab fa-youtube text-xl"></i>
                </a>
                <a
                  href="#"
                  className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                >
                  <i className="fab fa-linkedin-in text-xl"></i>
                </a>
              </div>
            </div>
            <div>
              <h3 className="text-xl font-bold mb-6">Quick Links</h3>
              <ul className="space-y-4">
                <li>
                  <a
                    href="https://readdy.ai/home/68fc91bc-34e7-47cc-8779-b3ad9976abda/8548099c-0e99-4419-8cfd-41bd85bb7724"
                    data-readdy="true"
                    className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                  >
                    Home
                  </a>
                </li>
                <li>
                  <a
                    href="#inventory"
                    className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                  >
                    Inventory
                  </a>
                </li>
                <li>
                  <a
                    href="#about"
                    className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                  >
                    About Us
                  </a>
                </li>
                <li>
                  <a
                    href="#testimonials"
                    className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                  >
                    Testimonials
                  </a>
                </li>
                <li>
                  <a
                    href="#contact"
                    className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                  >
                    Contact
                  </a>
                </li>
              </ul>
            </div>
            <div>
              <h3 className="text-xl font-bold mb-6">Our Services</h3>
              <ul className="space-y-4">
                <li>
                  <a
                    href="#"
                    className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                  >
                    Vehicle Sales
                  </a>
                </li>
                <li>
                  <a
                    href="#"
                    className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                  >
                    Financing Options
                  </a>
                </li>
                <li>
                  <a
                    href="#"
                    className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                  >
                    Vehicle Customization
                  </a>
                </li>
                <li>
                  <a
                    href="#"
                    className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                  >
                    Maintenance Services
                  </a>
                </li>
                <li>
                  <a
                    href="#"
                    className="text-gray-400 hover:text-white transition-colors duration-300 cursor-pointer"
                  >
                    Vehicle Consignment
                  </a>
                </li>
              </ul>
            </div>
            <div>
              <h3 className="text-xl font-bold mb-6">Newsletter</h3>
              <p className="text-gray-400 mb-6">
                Subscribe to receive updates on new arrivals and exclusive
                events.
              </p>
              <form className="mb-4">
                <div className="flex">
                  <input
                    type="email"
                    placeholder="Your email address"
                    className="w-full px-4 py-3 bg-gray-800 border-none rounded-l-lg focus:outline-none focus:ring-2 focus:ring-amber-500 text-white"
                  />
                  <button
                    type="submit"
                    className="bg-amber-500 text-white px-4 py-3 rounded-r-lg cursor-pointer hover:bg-amber-600 transition-colors duration-300"
                  >
                    <i className="fas fa-paper-plane"></i>
                  </button>
                </div>
              </form>
              <div className="flex space-x-4">
                <div className="flex items-center text-gray-400">
                  <i className="fab fa-cc-visa text-2xl"></i>
                </div>
                <div className="flex items-center text-gray-400">
                  <i className="fab fa-cc-mastercard text-2xl"></i>
                </div>
                <div className="flex items-center text-gray-400">
                  <i className="fab fa-cc-amex text-2xl"></i>
                </div>
                <div className="flex items-center text-gray-400">
                  <i className="fab fa-cc-paypal text-2xl"></i>
                </div>
              </div>
            </div>
          </div>
          <div className="border-t border-gray-800 pt-8">
            <div className="flex flex-col md:flex-row justify-between items-center">
              <p className="text-gray-400 text-sm mb-4 md:mb-0">
                &copy; {new Date().getFullYear()} Luxe Motors. All rights
                reserved.
              </p>
              <div className="flex space-x-6">
                <a
                  href="#"
                  className="text-gray-400 hover:text-white text-sm transition-colors duration-300 cursor-pointer"
                >
                  Privacy Policy
                </a>
                <a
                  href="#"
                  className="text-gray-400 hover:text-white text-sm transition-colors duration-300 cursor-pointer"
                >
                  Terms of Service
                </a>
                <a
                  href="#"
                  className="text-gray-400 hover:text-white text-sm transition-colors duration-300 cursor-pointer"
                >
                  Cookie Policy
                </a>
              </div>
            </div>
          </div>
        </div>
      </footer>

      {/* Floating Back to Top Button */}
      <button
        onClick={() => window.scrollTo({ top: 0, behavior: "smooth" })}
        className="fixed bottom-8 right-8 bg-amber-500 text-white w-12 h-12 rounded-full shadow-lg flex items-center justify-center hover:bg-amber-600 transition-colors duration-300 cursor-pointer"
      >
        <i className="fas fa-chevron-up"></i>
      </button>
    </div>
  );
};

export default App;
