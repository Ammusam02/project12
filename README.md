# project12
// App.jsx
import React, { useEffect, useState } from 'react';
import { useSearchParams } from 'react-router-dom';
import DoctorCard from './components/DoctorCard';
import Filters from './components/Filters';
import SearchBar from './components/SearchBar';

const API_URL = 'https://srijandubey.github.io/campus-api-mock/SRM-C1-25.json';

export default function App() {
  const [doctors, setDoctors] = useState([]);
  const [filteredDoctors, setFilteredDoctors] = useState([]);
  const [searchParams, setSearchParams] = useSearchParams();

  useEffect(() => {
    fetch(API_URL)
      .then(res => res.json())
      .then(data => {
        setDoctors(data);
      });
  }, []);

  useEffect(() => {
    applyFilters();
  }, [doctors, searchParams]);

  const applyFilters = () => {
    let result = [...doctors];
    const search = searchParams.get('search') || '';
    const moc = searchParams.get('moc');
    const specialties = searchParams.getAll('specialty');
    const sort = searchParams.get('sort');

  
  };

  return (
    <div className="p-4">
      <SearchBar searchParams={searchParams} setSearchParams={setSearchParams} />
      <div className="flex">
        <Filters searchParams={searchParams} setSearchParams={setSearchParams} />
        <div className="flex-1 grid gap-4">
          {filteredDoctors.map((doc, idx) => (
            <DoctorCard key={idx} doctor={doc} />
          ))}
        </div>
      </div>
    </div>
  );
}
